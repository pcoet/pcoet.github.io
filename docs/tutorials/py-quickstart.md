---
tags:
  - Python
---

# Python quickstart

This tutorial shows you how to use
[venv](https://docs.python.org/3/library/venv.html) to set up a Python virtual
environment on macOS.

To complete this tutorial, you need Python 3.3 or higher. To check your Python
version, run

    python3 --version

## (Optional) Upgrade Python

You might want to upgrade your version of Python before creating a virtual
environment. If you have [Homebrew](https://brew.sh/), you can install a
recent version of Python using this command:

    brew install python

To upgrade a Homebrew version of Python, run the following command:

    brew upgrade python

Alternatively, you can download the most recent version of Python from the
[Python downloads page](https://www.python.org/downloads/).

## Create a virtual environment

Run the following command in your project directory, replacing
`<quickstart-env>` with the name you want to use for your virtual environment:

    python3 -m venv <quickstart-env>

## Activate the virtual environment

To activate the virtual environment, run the following command, replacing
`<quickstart-env>` with the name you used for your virtual environment:

    source <quickstart-env>/bin/activate

Now you can use the `python` command, rather than `python3`:

    python --version

The `python` alias points to whatever version of Python you used to create the
virtual environment.

## (Optional) Install dependencies

With your virtual environment activated, you can use `pip` (instead of `pip3`)
to install dependencies that are only available in the virtual environment. For
example:

    pip install pydantic

The library files will be installed in your virtual environment in a location
like `<quickstart-env>/lib/python3.<XX>/site-packages/pydantic`. 

## (Optional) Create `requirements.txt`

If you want your users to have the same dependencies that you do in your virtual
environment, you can create a `requirements.txt` file that specifies dependency
versions:

    python -m pip freeze > requirements.txt

Users can install these dependencies with the following command:

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

To learn more about virtual environments, see the following resources:

* [Virtual Environments and Packages](https://docs.python.org/3/tutorial/venv.html)
* [venv — Creation of virtual environments](https://docs.python.org/3/library/venv.html)