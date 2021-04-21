---
title: Anaconda
date: 2020-01-21 00:00:00 Z
tags:
- Python
---

# 目录

>
- root
    - Lib : Python 自带的包目录,例如 os, sqlite3 等等
        - site-packages : 所有通过 pip 等工具下载的包都会下载到当前目录下
            - ...
        - ...
    - envs : Anaconda 管理的环境都会在 envs 下创建几个子目录
        - MyEnv
            - Lib
                - site-packages
            - ...
        - ...
    - Scripts
        - conda.exe
    - python.exe
    - ...

# conda -h

[Anacodna之conda与 virtualenv使用教程](https://zhuanlan.zhihu.com/p/40012999)

`conda -h > conda-h.txt`

```
usage: conda-script.py [-h] [-V] command ...

conda is a tool for managing and deploying applications, environments and packages.

Options:

positional arguments:
  command
    clean        Remove unused packages and caches.
    config       Modify configuration values in .condarc. This is modeled
                 after the git config command. Writes to the user .condarc
                 file (C:\Users\ratsafalig\.condarc) by default.
    create       Create a new conda environment from a list of specified
                 packages.
    help         Displays a list of available conda commands and their help
                 strings.
    info         Display information about current conda install.
    init         Initialize conda for shell interaction. [Experimental]
    install      Installs a list of packages into a specified conda
                 environment.
    list         List linked packages in a conda environment.
    package      Low-level conda package utility. (EXPERIMENTAL)
    remove       Remove a list of packages from a specified conda environment.
    uninstall    Alias for conda remove.
    run          Run an executable in a conda environment. [Experimental]
    search       Search for packages and display associated information. The
                 input is a MatchSpec, a query language for conda packages.
                 See examples below.
    update       Updates conda packages to the latest compatible version.
    upgrade      Alias for conda update.

optional arguments:
  -h, --help     Show this help message and exit.
  -V, --version  Show the conda version number and exit.

conda commands available from other packages:
  build
  convert
  debug
  develop
  env
  index
  inspect
  metapackage
  render
  server
  skeleton
  verify
```