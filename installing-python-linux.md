# Installing Python on Linux

Hello!

This document provides a walkthrough to set up a Python development environment for [CS41](https://stanfordpython.com) on Linux. Alternate versions of this guide exist for [macOS](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-macos.md) and [Windows](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-windows.md) development.

## Overview

In this course, you'll be writing lots of Python code, so it's important to get your development environment set up and ready-to-go. Moreover, we will sometimes need to install dependencies and packages, so we want to make sure that everything is installed to the right place as well. The tools we develop in this document will also be useful for any external development you might pursue in Python.

Throughout this document, we will:

1. Install Python 3.9.2
2. Create a virtual environment using this version of Python.
3. Inside this environment, install useful packages.

Let's get started!

## Prerequisite

We assume that you have a basic familiarity with the command line. We understand that not everyone will feel comfortable with the command line, because it is covered starting in CS107. However, I highly recommend using Nick Troccoli's amazing [CS107 resources](https://web.stanford.edu/class/archive/cs/cs107/cs107.1214/resources/) for this quarter if you feel less experienced, particular the section titled "Common Unix Commands."

## Install Python 3.9.2

On different Linux systems, there are a couple of different ways to install and manage packages. We'll cover `apt-get` here, as well as how you can install from source.

### Installing with `apt-get` (Ubuntu, Debian)

`apt-get` is Linux's Advanced Package Tool, and is very useful for installing, managing, upgrading, and removing packages on Debian, Ubuntu, and a few other Linux distributions. We'll use [Felix Krull's PPA](https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa) to install specific Python versions. 

```
$ sudo add-apt-repository ppa:deadsnakes/ppa
$ sudo apt-get update
$ sudo apt-get install python3.9
$ sudo apt-get install python3.9-venv
```

On Debian, we'll just have to `sudo apt-get install python3` and hope for the best. Also note that this might install a different version of Python 3.9, but we won't worry about that here.

### Installing with `yum` (RedHat, CentOS)

Other Linux distributions use a different package manager, `yum`. We don't have any test devices with these Linux distributions, so you're on your own here. There is a reasonably good tutorial for CentOS [here](https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-local-programming-environment-on-centos-7).

### Other Linux package managers

The world of Linux distributions is unfathomably large. If you can pull off a Python 3.9 install on your distribution of choice, more power to you. However, we recommend building from source.

### Installing from source

Installing Python from source follows the same pattern as most other source installations.

First, download the source tarball (either [gzipped](https://www.python.org/ftp/python/3.9.2/Python-3.9.2.tgz) or [XZ compressed](https://www.python.org/ftp/python/3.9.2/Python-3.9.2.tar.xz)). Unzip the files and `cd` into the unzipped directory.

To build Python, just execute the usual commands:

```
$ ./configure
$ make 
$ make test
$ sudo make install
```

*Note: If you want to install Python to a non-standard location, you can `./configure --prefix=/some/other/directory` in order to, say, not overwrite a system-installed Python, which might be useful for distributions like CentOS*

More information on the actual installation process can be found in the tarball's README.

## Follow the macOS Instructions

From here, the instructions are almost exactly the same as the [macOS](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-macos.md) instructions. Follow those instructions, with the following differences.

## Credit
Much of this handout was based on a similar handout written by Sam Redmond (@samredmond)
