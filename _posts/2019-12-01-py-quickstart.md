---
title: Set up a Python environment
category: Python
---

*Last updated: December 8, 2019*

The "Getting Started" section below walks you through the process of creating a simple Python app and setting up a virtual environment to run it in. The "Things to know" section provides additional context and other tips to get you up and running with Python.

## Getting started ##

1. Make sure you have Python 3 installed: `python3`
    * If you don't, install it. For Mac, see [Installing Python 3 on Mac OS X](https://docs.python-guide.org/starting/install3/osx/).
1. Create a directory for your app: `mkdir <my-app>`
1. Create an app.py file: `cd <my-app> && touch app.py`
1. Add the following code to app.py:

   ```python
   name = ""

   while name == "":
       name = str(input("What's your name?\n"))
       if name != "":
           print("Hello, " + name)
   ```

1. Create and activate a virtual environment:
    * `python3 -m venv venv`
        * Note: If you put the app under version control in Git, you should ignore the **venv** directory.
    * `source venv/bin/activate`
1. Run the application to see how it works: `python3 app.py`
1. When you're finished, deactivate the environment:
  * `deactivate`

## Things to know ##

*A lot of the content below is excerpted or adapted from the official Python docs.*

### venv ###

A virtual environment is a Python environment such that the Python interpreter, libraries, and scripts installed into it are isolated from those installed in other virtual environments, and (by default) any libraries installed in a “system” Python, i.e., one which is installed as part of your operating system.

Common installation tools such as [Setuptools](https://setuptools.readthedocs.io/en/latest/) and [pip](https://pypi.org/project/pip/) work as expected with virtual environments. In other words, when a virtual environment is active, they install Python packages into the virtual environment without needing to be told to do so explicitly.

You create a virtual environment with the `venv` command:

```shell
python3 -m venv /path/to/new/virtual/environment
```

To activate your virtual env, run:

```shell
source <venv>/bin/activate
```

To deactivate, run:

```shell
deactivate
```

You don’t specifically need to activate an environment; activation just prepends the virtual environment’s binary directory to your path, so that “python” invokes the virtual environment’s Python interpreter and you can run installed scripts without having to use their full path. However, all scripts installed in a virtual environment should be runnable without activating it, and run with the virtual environment’s Python automatically.

### Modules ###

To import a module:

```python
import my_module
```

Also, you can import names from a module directly into the importing module’s symbol table:

```python
from my_module import my_func
```

This imports all names except those beginning with an underscore:

```python
from my_module import *
```

Note that in general the practice of importing `*` from a module or package is frowned upon, since it often causes poorly readable code.

For efficiency reasons, each module is only imported once per interpreter session. Therefore, if you change your modules, you have to restart the interpreter &mdash; or, if it’s just one module you want to test interactively, use `importlib.reload()`, e.g. `import importlib; importlib.reload(modulename)`.

When you run a Python module with

```python
python mod.py <arguments>
```

the code in the module will be executed, just as if you imported it, but with the `__name__` set to `"__main__"`. That means that by adding something like this at the end of your module...

```python
if __name__ == "__main__":
    import sys
    some_function((sys.argv[1])
```

...you can make the file usable as a script as well as an importable module, because the code that parses the command line only runs if the module is executed as the “main” file

### Packages ###

Packages are a way of structuring Python’s module namespace by using dot syntax. For example, the module name A.B designates a submodule named B in a package named A.

An `__init__.py` file is required to make Python treat a directory as containing a package. In the simplest case, `__init__.py` can just be an empty file, but it can also execute initialization code for the package

### Style ###

Use 4-space indentation, and no tabs.

Name your classes and functions consistently; the convention is to use CamelCase for classes and lower_case_with_underscores for functions and methods.