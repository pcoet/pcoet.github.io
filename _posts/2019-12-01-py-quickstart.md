---
title: Set up a Python environment
category: Python
last_updated: June 7, 2020
---

This post explains how to create a Python environment using [Conda](https://docs.conda.io/en/latest/) and how to install [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/index.html) in that environment.

## What is Conda?

Conda is a package and environment management tool and an alternative to [virtualenv](https://pypi.org/project/virtualenv/). Conda is distributed with [Anaconda](https://docs.anaconda.com/), a Python data science platform. Once you have Conda installed, you can use it to create Python environments and to install packages. If you want to install packages through [pip](https://pypi.org/project/pip/), you can do that, too. pip is available through the Python distribution included with Anaconda.

## Update or install Conda

If you don't already have Conda, you'll need to install it. It's available as part of the full Anaconda distribution, which includes Python and more than 200 libraries, or as part of Miniconda, which is a lightweight version of Anaconda that includes Python and a minimal set of libraries.

Unless you need a fully provisioned data science environment out of the box, [install Miniconda](https://docs.conda.io/en/latest/miniconda.html). Also, if you don't have a specific reason to use Python 2, install the Python 3 version.

Once you have Conda installed, you can update it by running:

    conda update -n base conda

## Learn more about the conda installation

After you install Conda, you can learn more about your Conda configuration by running:

    conda info

To see the list of packages that are included with Miniconda (or Anaconda), run:

    conda list

To see a list of environments, run:

    conda env list

A new Conda installation includes a **base** environment. You should create additional environments for your actual projects.

## Create an environment

To create a new environment, run:

    conda create --name <envname> python=<major-version>.<minor-version>

For example:

    conda create --name my_env python=3.7

## Activate the environment

To activate the environment, run:

    conda activate <envname>

With the environment activated, the Python binary should be available. If you run `python --version`, you should see the version you specified in creating the environment, e.g. 3.7.

## Install JupyterLab

To install JupyterLab, run:

    conda install -c conda-forge jupyterlab

You can test the installation by running:

    jupyter lab

## Deactivate the environment

When you're finished working in the environment, deactivate it:

    conda deactivate

## Remove the environment

When you no longer need the environment, you can delete it by running:

    conda env remove --name <envname>

## Resources

* [Conda docs](https://docs.conda.io/en/latest/)
* [JupyterLab Documentation](https://jupyterlab.readthedocs.io/en/stable/index.html)

### Videos

* [Corey Schafer: Python Tutorial: Anaconda - Installation and Using Conda](https://www.youtube.com/watch?v=YJC6ldI3hWk)
* [Google Cloud Platform: Jupyter Tips and Tricks (AI Adventures)](https://www.youtube.com/watch?v=2eCHD6f_phE&list=TLPQMDcwNjIwMjCsHwENipEOJw&index=2)
* [Google Cloud Platform: Which Python Package Manager Should You Use? (AI Adventures)](https://www.youtube.com/watch?v=3J02sec99RM)
* [Tech With Tim: Anaconda Tutorial 2019 - Python Virtual Environment Manager](https://www.youtube.com/watch?v=mIB7IZFCE_k)