---
tags:
  - Python
---

# Python quickstart

This tutorial shows you how to set up a Python virtual environment on macOS
using [venv](https://docs.python.org/3/library/venv.html). 

## Upgrade Python

To complete this tutorial, you need Python 3.3 or higher. To check your Python
version, run

    python3 --version

If you're using the default macOS version of Python, consider installing a more
recent version. If you have [Homebrew](https://brew.sh/), you
can install Python like this:

    brew install python

To upgrade a Homebrew version of Python, run

    brew upgrade python

Alternatively, you can download the most recent version of Python from the
[Python downloads page](https://www.python.org/downloads/).

## Create a virtual environment

Run the following command in your project directory, replacing
`quickstart-env` with the name you want to use for your virtual environment:

    python3 -m venv quickstart-env

## Activate the virtual environment

    source quickstart-env/bin/activate

Now you can use the `python` command, rather than `python3`. For example:

    python --version

The `python` alias points to whatever version of Python you used to create the
virtual environment.

## (Optional) Install a dependency

With your virtual environment activated, you can use `pip` (instead of `pip3`)
to install a dependency that's only available in the virtual environment. For
example:

    pip install pydantic

The library files will be installed in your virtual environment in a location
like this: `<my-env>/lib/python3.<XX>/site-packages/pydantic`. 

## (Optional) Create `requirements.txt`

To ensure that all users of your package have the same dependency versions, you
can create a `requirements.txt` file:

    python -m pip freeze > requirements.txt

The `requirements.txt` file specifies the dependencies for your project.
If you distribute `requirements.txt`, users can install the exact dependency
versions you're using in your virtual environment:

    python -m pip install -r requirements.txt

For more information, see
[Managing Packages with pip](https://docs.python.org/3/tutorial/venv.html#managing-packages-with-pip).

## Deactivate the virtual environment

When you're done working in your virtual environment, deactivate it:

    deactivate

## Learn more

In some cases, you might need to manage multiple versions of Python on the
same machine. For these cases, you can use
[pyenv](https://github.com/pyenv/pyenv).

You can configure VS Code to use the Python version in your virtual environment.
To learn more, see
[Python in Visual Studio Code](https://code.visualstudio.com/docs/languages/python#_environments).

To learn more about virtual environments, see
[Virtual Environments and Packages](https://docs.python.org/3/tutorial/venv.html)
and the [venv library docs](https://docs.python.org/3/library/venv.html).