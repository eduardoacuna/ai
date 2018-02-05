# Setting up a python environment

This guide covers how to set up a python environment for developing machine learning programs.

## Installing python 3

The python code used in this repository runs with the third version of python.

**Mac**

Install [homebrew](https://brew.sh/) and run the following command in the Terminal app:

```
$ brew install python3
```

**Linux**

Use the package manager of your preference, like apt-get or pacman to install:

```
$ apt-get install python3
```

Verify that python has been installed correctly. After running the `python3` command you should see something like the following:

```
$ python3
Python 3.6.4 (default, Jan  6 2018, 11:49:38)
[GCC 4.2.1 Compatible Apple LLVM 8.0.0 (clang-800.0.42.1)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

## Setting up a virtual environment

Python provides support for virtual environments to manage a local python distribution and library dependencies.

Run the following command to create a virtual environment named `dev`:

```
$ python3 -m venv dev
```

**troubleshooting:** In some linux distributions you'll have to install the `venv` module before running the command above. In Debian with apt-get you could run `apt-get install python3-venv`.

This will create the `dev` folder where the complete python distribution and dependencies is installed.

To activate this newly created environment we have to source the `activate` script inside `/dev/bin`:

```
$ source dev/bin/activate
```

This updates the `PATH` environment variable to identify the virtual environment binaries before the ones installed globally in the system. It also exposes the `deactivate` command, which will revert the state of the shell like it was before sourcing the `activate` script.

Notice that while being in the `dev` environment we can use the `python` command to run python 3, it doesn't matter if the system version of python is 2. To verify this the following command should print the current directory followed by `/dev/bin/python`:

```
(dev) $ which python
```

## Installing some libraries

Now let's install some useful libraries for doing machine learning! We can use the `pip` command to do this easily:

```
(dev) $ pip install numpy scipy matplotlib ipython jupyter pandas
```

**troubleshooting:** In some linux distributions the `wheel` library is required to be installed before executing the command above. It can be installed with `pip install wheel`.

To verify these libraries are in fact installed we can run `pip list`:

```
(dev) $ pip list
Package            Version
------------------ -------
appnope            0.1.0
bleach             2.1.2
cycler             0.10.0
decorator          4.2.1
entrypoints        0.2.3
html5lib           1.0.1
ipykernel          4.8.0
ipython            6.2.1
ipython-genutils   0.2.0
ipywidgets         7.1.1
jedi               0.11.1
Jinja2             2.10
jsonschema         2.6.0
jupyter            1.0.0
jupyter-client     5.2.2
jupyter-console    5.2.0
jupyter-core       4.4.0
MarkupSafe         1.0
matplotlib         2.1.2
mistune            0.8.3
nbconvert          5.3.1
nbformat           4.4.0
notebook           5.4.0
numpy              1.14.0
pandas             0.22.0
pandocfilters      1.4.2
parso              0.1.1
pexpect            4.3.1
pickleshare        0.7.4
pip                9.0.1
prompt-toolkit     1.0.15
ptyprocess         0.5.2
Pygments           2.2.0
pyparsing          2.2.0
python-dateutil    2.6.1
pytz               2017.3
pyzmq              16.0.4
qtconsole          4.3.1
scipy              1.0.0
Send2Trash         1.4.2
setuptools         28.8.0
simplegeneric      0.8.1
six                1.11.0
terminado          0.8.1
testpath           0.3.1
tornado            4.5.3
traitlets          4.3.2
wcwidth            0.1.7
webencodings       0.5.1
widgetsnbextension 3.1.3
```

As we can see, it installed all the libraries and their dependencies. Let's test this by importing `numpy` from the iPython REPL and creating a zero array with 5 elements:

```
(dev) $ ipython
In [1]: import numpy as np

In [2]: np.zeros(5)
Out[2]: array([0., 0., 0., 0., 0.])
```

## Using virtual environments with version control

It's not convenient to have the entire python distribution + libraries in version control. The convention is to use the `pip freeze` command to generate a `requirements.txt` file which we can commit into version control:

```
(dev) $ pip freeze > requirements.txt
```

This file will contain the name of the libraries and the precise version is supposed to be used in the project. The `dev` directory won't be under version control, so each developer working on the repository will have to set up it's own virtual environment as above and then run the following command to install the project dependencies:

```
(dev) $ pip install -r requirements.txt
```
