# Automation Workbench Scripts

This repository contains a collection of useful automation scripts and tools that can be imported into the Automation Workbench of [Binary Ninja Sidekick](https://sidekick.binary.ninja). These scripts are designed to enhance your reverse engineering workflow by automating common tasks and providing additional functionality.

## Overview

The Automation Workbench in Binary Ninja Sidekick allows you to run custom scripts and provide tools for the AI assistant in the Analysis Console. This repository serves as a curated collection of ready-to-use scripts for various reverse engineering tasks.

## How to Import Scripts

To use these scripts in Binary Ninja Sidekick:

1. Download the scripts from this repository
2. Open Binary Ninja Sidekick
3. Navigate to the Automation Workbench
4. Click "Import Scripts" from the hamburger menu

## Script Categories

### Vulnerability Research

Scripts to assist in vulnerability research.

| Script Name | Description | Author |
|-------------|-------------|--------|
| `Search CVEs` | Searches NVD for CVEs related to a given binary and version | [Vector 35](https://github.com/Vector35) |

### Projects

Scripts for indexing and search project files. (Note: These scripts require a version of Binary Ninja that supports the project API.)

| Script Name | Description | Author |
|-------------|-------------|--------|
| `Index Project Files` | Creates a searchable index of files in the current Binary Ninja project using the Whoosh library | [Vector 35](https://github.com/Vector35) |
| `Search Project Files` | Searches and returns content from the project files | [Vector 35](https://github.com/Vector35) |

## Contributing

We welcome contributions to this repository. If you have developed a useful script for Binary Ninja Sidekick, please consider submitting a pull request.

## License

All scripts in this repository are provided under [LICENSE INFORMATION].
