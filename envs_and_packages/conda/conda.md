# CONDA

Utility to create splitted environments, each containing their own files, packages and dependencies.[Official reference link](https://docs.conda.io/projects/conda/en/stable/user-guide/tasks/manage-environments.html)

[TOC]

## Environment creation

Environments are created from CLI or using an `environment.yaml` file:

````bash
conda create --name my_env [dependencies dependencies=dep_version]
#example: conda create -n my_env python=3.9 
#Will ask to proceed (y/n)
````

Using `conda env list` you list all the available environments in your system.

```yaml
name: myenv
channels:
  - conda-forge
dependencies:
  - python
  - numpy
```

To create the environment from the YAML file, use `conda env create --file environment.yml`

Environments could be created and stored into a file:

```bash
conda create --prefix ./envs jupyterlab=3.2 matplotlib=3.5 numpy=1.21
conda activate ./envs
```

## Environment installation / Updating

Packages can be installed into an existing environment:

```bash
conda create -n myenv python
conda install -n myenv scipy
```

> Installing one program/dependency at a time can lead to dependency conflicts. Install all the dependencies at the same time.

Environments can be also updated using:

```bash
conda env update --file environment.yml  --prune
#prune -> remove no longer used dependencies
```

## Activate environment

The activation makes all the necesary changes to start using the environment.

To enable the environment, use `conda activate my_env_name`.  

## Conda commands

| Command                                    | Description                                                  |
| ------------------------------------------ | ------------------------------------------------------------ |
| `conda create -n env_name [dependencie/s]` | Create a new environment                                     |
| `conda install -n env_name dependency`     | Install dependency into an environment                       |
| `conda activate env_name`                  | Activate an environment                                      |
| `conda info`                               | Show system information                                      |
| `conda env list`                           | List available environments. Shortcut of `conda info --envs` |
|                                            |                                                              |
|                                            |                                                              |

## Advance utilities

### .condarc

The `.condarc` file can override the default user configuration of Conda.

```bash
#.condarc
conda config --set env_prompt '({name})'
```

### spec-files

Spec files are used to generate identical environments:

```bash
conda list --explicit > spec-file.txt
# create a container using the spec-file:
conda create --name myenv --file spec-file.txt
#or
conda install --name myenv --file spec-file.txt
```

### Cloning an environment 

TBD

### Targeting platforms

Using `--platform <platform_name>` you can generate an environment for a different platform. Conda will use Rossetta underneath to emulate the execution of that environment.
