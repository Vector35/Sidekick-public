# Binary Ninja Query Language

The Binary Ninja Query Language (BNQL) is designed to retrieve Binary Ninja API objects that represent the functions, variables, sections, strings, symbols, and various other entities of a binary. Queries make use of relationships between these entities to efficiently find the right objects. Queries may also access object indexes, which contain lists of objects pertaining to user-defined topics.

Queries do not replace the need to analyze decompiled code or data. A typical analysis involves:


1. Writing queries to find relevant code, data, or metadata
2. Examining the decompiled code and data returned by the query
3. Based on the findings, deciding what to query next

## Query Structure

A single step query has the following pattern:

```
/<relationship>::<object_type>[<predicate>]
```

### Object Types

The `<object_type>` part selects the type of object. A wildcard `*` matches any object type. The complete list of objects types and their corresponding API classes are:

* `function`: Functions defined in the binary (Function)
* `datavar`: Variables stored in the data sections (DataVariable)
* `variable`: Local variables and parameters, when querying within a function (Variable)
* `string`: String literals which may or may not be referenced by code or data (StringReference)
* `symbol`: Named entities (Symbol or CoreSymbol)
* `callable`: Entities that can be called by a function (Function, Symbol, CoreSymbol)
* `block`: Basic blocks (BasicBlock)
* `instruction`: IL instructions (LowLevelILInstruction, MediumLevelILInstruction, HighLevelILInstruction)
* `type`: Data types and structures (Type and its subclasses)
* `segment`: Memory segments (Segment)
* `section`: Named sections (Section)
* `external-library`: External library references (ExternalLibrary)
* `external-location`: Symbol that refers to an external location (ExternalLocation)
* `component`: Logical grouping of functions and data (Component)
* `comment`: User comments at specific addresses (N/A)
* `index`: User-defined collections of the objects along with per-object metadata (N/A)

### Predicates

The `[<predicate>]` part of the query filters selected objects with a logical expression. The logical operators are `and`, `or`, and `not`, and parentheses are used to group expressions to control the order of evaluation. Predicates test the attributes of an object using relational operators:

* `<`: Less than
* `>`: Greater than
* `<=`: Less than or equal to
* `>=`: Greater than or equal to
* `==`: Equal to
* `!=`: Not equal to
* `~=` : Matches (regular expression matching)

Object attributes are denoted using `@`. The available attributes are determined by the corresponding Binary Ninja API object. For example, an instruction object has an `@operation` attribute and a function object has a `@name` attribute.

For simple queries we can omit the relationship part. For example:

* To find a function named "main": `/function[@name == 'main']`
* To find strings containing "error": `/string[@value ~= 'error']`
* To find data variables at a given address: `/data[@address == 0xbaa800]`

Predicate expressions may also include relationship tests. But first we must introduce relationships.

### Relationships

The `/<relationship>::` part of the query is used to step from a set of source objects to a set of target objects by traversing the specified relationship. For example, the following query selects the callees of the source function.

```
/function[@name == 'source']/calls::function
```

Relationships may also be used inside predicates where they filter objects based on the existence of relationships. For relationships relative to the object, we omit the leading `/`. The following example selects strings using relationships: 1) the string must be used by functions with “server” in the name and 2) not used by functions with “log” in the name:

```
/string[used-by::function[@name ~= 'server] and not used-by::function[@name ~= 'log']]
```

Note: The first step of a query begins at the BinaryView object. Thus, a query like `/symbol` says “given the current binary view, select symbol objects contained in the binary view”.

Here is the complete list of the available relationships for each object type:

**(BinaryView)**

* `contains`: Get all top-level objects in the binary
* `hlil`: Get high-level IL instructions
* `mlil`: Get medium-level IL instructions
* `llil`: Get low-level IL instructions

**function**

* `calls`: Callables ('function', 'symbol', or 'callable') called by this function
* `called-by`: Functions that call this function
* `contains`: Get specific basic blocks, local variables (including parameters), and IL instructions; using predicates to specify criteria
* `defined-in`: None (functions are top-level)
* `hlil`: Get high-level IL instructions
* `mlil`: Get medium-level IL instructions
* `llil`: Get low-level IL instructions
* `uses`: Get data variables and strings used in the function
* `used-by`: Get functions using this function
* `reads`: Get variables read by the function
* `writes`: Get variables written by the function
* `references`: Get address-taken variables and type references
* `has-type`: Get function type
* `has-symbol`: Get function symbol
* `navigated-to`: What the user has navigated to from this function

**block**

* `next`: Get successor blocks
* `prev`: Get predecessor blocks
* `defined-in`: Get containing function
* `contains`: Get instructions
* `uses`: Get data variables and strings used in the block
* `references`: Get address-taken variables

**type**

* `references`: Get referenced types (e.g., struct members)
* `referenced-by`: Get objects using this type
* `inherits`: Get base types
* `implements`: Get implemented interfaces

**data**

* `has-type`: Get variable type
* `uses`: Get data variables referenced by the data variable
* `used-by`: Get functions/variables using this data
* `has-symbol`: Get associated symbol
* `references`: Get type and symbol references

**string**

* `used-by`: Get functions using this string
* `references`: None (strings don't reference other objects)

**instruction** For MLIL and HLIL instructions:

* `reads`: Get variables read
* `writes`: Get variables written
* `uses`: Get all variables accessed
* `references`: Get address-taken variables

**variable**

* `has-type`: Get variable type
* `defined-in`: Get containing function
* `used-by`: Get instructions using this variable

**component**

* `contains`: Get child components
* `defined-in`: Get parent component

**segment**

* `contains`: Get functions, data, and strings in this region

**section**

* `contains`: Get functions, data, and strings in this region

**symbol**

* `has-symbol`: Get objects with this symbol
* `called-by`: Functions that call this symbol

**callable**

* `calls`: Get callables called by this callable
* `called-by`: Get callables that call this callable

**index**

* `contains`: Get indexed objects

### Complex Queries

A query may consist of multiple steps and nested predicate expressions. Steps are used to traverse and select the destination objects. Predicates are used to filter objects selected at the current step.

The following type of query returns objects at step C:

```
/A/B/C
```

The following type of query returns objects at step A, which satisfied B, which in turn satisfied C:

```
/A[B[C]]
```

## The Default Relationship

If the `/<relationship>::` part of a query step is omitted, the default relationship is `contains`. In other words, `/` is syntactically equivalent to `/contains::`. The `contains` relationship is useful for navigating the hierarchy of a decompiled binary. For example, sections contain functions and data, functions contains basic blocks, basic blocks contain instructions, etc.

## Local Variables versus Data Variables

In Binary Ninja, local variables include function parameters, register variables, and stack variables. Data variables are values stored in the data sections and may be used anywhere in the binary. Functions can read/write both local and global variables.

## Callables

A callable is an object that can be called by a function. Callables include functions and symbols. The `callable` object type is used to refer to both functions and symbols.

To find a call target by name, use the `callable` object type (or the `*` wildcard) which will find any function or symbol that matches. Otherwise, you can limit the search to functions defined in the binary or to symbols imported from external libraries using the `function` or `symbol` object types.

```
/.../calls::callable[@name == 'target']
```

In contrast, the `called-by` relationship always selects functions because only functions defined in the binary have explicit call sites.

## Common Queries

Finding Suspicious Functions:

```
/function[@name ~= '(crypt|decrypt|encode|decode)']

/function[calls::*[@name == 'malloc'] and calls::*[@name == 'memcpy']]

/function[uses::string[@value ~= 'password|secret|key']]
```

Analyzing Data Flow:

```
/function[@name == 'main']/reads::variable[has-type::type[@name ~= 'char\*']]

/data[@address >= 0x400000 and @address < 0x401000]/used-by::function

/string[used-by::function[@name ~= 'network|socket|connect']]
```

Vulnerability Research:

```
/function[calls::function[@name ~= '(strcpy|strcat|sprintf)']]

/function[uses::data[@value ~= '(%s|%x|%p)']]

/function[not calls::function[@name ~= 'validate|check|verify']]
```

Code Structure Analysis:

```
/function[@size > 1000]/block[@outgoing_edge_count > 5]

/function[calls::function[@name == 'malloc'] and not calls::function[@name == 'free']]

/function[@name ~= 'init|setup']/calls::function
```

Cross-References:

```
/string[@value ~= 'error']/used-by::function/calls::function

/data[@section == '.data']/used-by::function[@name ~= 'handler']

/function[@name == 'main']/calls::function/uses::string
```

