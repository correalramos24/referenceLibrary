# uv

This document contains the main features of uv to manage virtual environments,
project development and dependencies in Python.

Oficial webpage: https://docs.astral.sh/uv/

## Introduction

10-100x faster than `pip`.

Installation: `curl -LsSf https://astral.sh/uv/install.sh | sh`.

Capabilities: 
* Install Python versions
* Execute Python scripts with dependencies
* Manage projects
* Install and use python packages

## Capabilities

### Execute Python scripts

Scripts may be executed without any project related. On-the-fly Python dependencies can be managed by uv.

````bash
# Run simple script (may add any parameters)
uv run script-name.py

# Run with specific dependencies:
 uv run --with <package name> script-name.py

# Run with specific python version:

````

### Manage projects

A project can be initiated using `uv init project_name` or use `uv init` in a already created folder.
