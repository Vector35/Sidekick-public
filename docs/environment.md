# Setting Up a Virtual Environment

Sidekick is fully supported using the Python packaged with BinaryNinja, which is the preferred environment for running Sidekick.
However, BinaryNinja supports using other Python environments, which can be configured using these instructions.

## Create the Environment

The following instructions use `conda`, but any virtual environment can be used.  Create the environment with the following command:

> NOTE: The easiest way to install `conda` on MacOS is to use `brew install miniforge`.

```sh
conda create -n sidekick-beta python=3.9 packaging
```

## Install the Required Packages

The plugin requires Python 3.9 or later and the following packages:

```txt
requests>=2.28.2
networkx>=3.0.0
pygments>=2.14.0
intervaltree>=3.0.2
sentence-transformers>=2.2.2
scikit-learn>=1.1.3
pyjarowinkler>=1.8
```

## Configure BinaryNinja to Use the Environment

Use a separate `BN_USER_DIRECTORY` directory for the beta test.

1. Update your `settings.json` file to refer to the `sidekick-beta` environment.

2. Activate the environment:

    ```sh
    conda activate sidekick-beta
    ```

3. Locate the paths you will need for the `settings.json` file. For example, to find the site packages directory:

    ```sh
    python -c 'import site; print(site.getsitepackages()[0])'
    ```

4. Set the paths in the `settings.json`:

    ```json
    {
        "python.binaryOverride" : "/opt/homebrew/Caskroom/miniforge/base/envs/sidekick-beta/bin/python3.9",
        "python.interpreter" : "/opt/homebrew/Caskroom/miniforge/base/envs/sidekick-beta/lib/libpython3.9.dylib",
        "python.virtualenv" : "/opt/homebrew/Caskroom/miniforge/base/envs/sidekick-beta/lib/python3.9/site-packages"
    }
    ```
