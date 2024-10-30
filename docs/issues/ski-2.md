# Sidekick Issue 2: Python Package Requirements Conflicts During Installation

## Issue Summary

When installing the Sidekick plugin or its updates, you may encounter errors in the Binary Ninja log describing requirements for specific versions of Python modules that Sidekick uses.

For example,

`tokenizers>=0.20,<0.21 is required for a normal functioning of this module, but found tokenizers==0.19.1.`

## Required Actions

To resolve this issue, try the following:

* Close Binary Ninja
* Within your Python site-packages directory (within your configured Python environment for Binary Ninja), remove any older versions of the conflicting package (e.g. `tokenizers-0.19.1.dist-info`).
* Open Binary Ninja
* Re-install the Sidekick plugin

If that does not work, then try the following:

* Close Binary Ninja
* Remove the entire contents of your Python site-packages directory (within your configured Python environment for Binary Ninja)
* Open Binary Ninja
* Re-install the Sidekick plugin

!!! Note

    This will cause all other installed Python plugins with Python dependencies to no longer work, so you will need to re-install them as well.

If that does not work, then try the following:

* Close Binary Ninja
* Create a new folder that you will use as your BN User Directory
* Copy your Binary Ninja license file to the new folder
* In a terminal, set the BN_USER_DIRECTORY environment variable to the new folder
* In the same terminal, launch Binary Ninja
* Install the Sidekick plugin

If the above steps still do not work, then [contact us](mailto:sidekick@vector35.com).

## Other Information

Some users have found that other installed Binary Ninja plugins may hold locks on certain Python modules that prevent Sidekick from being updated or installed properly. If this happens, then one solution is to manually install the Sidekick dependencies as follows:

* First, obtain the list of Python packages required by the version of Sidekick you are trying to install. To do this, install or update the Sidekick plugin through the Binary Ninja Plugin Manager. During installation, the Plugin Manager will emit a log message containing the list of Python package dependencies being installed.
* Next, close Binary Ninja
* Open a terminal
* Using the version of Python configured in your Binary Ninja application, manually install the required packages according to the following example:

```sh
/path/to/your/python3 -m pip --isolated --disable-pip-version-check install --upgrade --upgrade-strategy only-if-needed --target $BN_USER_DIRECTORY/python310/site-packages $REQUIRED_PACKAGES
```

!!! note

    Replace `/path/to/your/python3` with the actual path to your version of Python. Replace $BN_USER_DIRECTORY with the path to your Binary Ninja User Directory. Replace $REQUIRED_PACKAGES with the list of Python package requirements for Sidekick. Instead of listing all Python package requirements in a single command, you can add them to a text file and then specify that text file path on the pip command line using the `-r` option.
