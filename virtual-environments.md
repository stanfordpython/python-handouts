# Virtual Environments Primer

This document is meant as a supplement to our Installing Python series:

- [Installing Python for macOS](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-macos.md)
- [Installing Python for Linux](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-linux.md)
- [Installing Python for Windows](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-windows.md)

## Using virtual environments

Once you have a virtual environment set up for a project or for a course, there's only one important thing to remember. **Activate your virtual environment every time you open a new shell.** We'll see what this means and how to do this later in this document. For now, if you only take away one thing, it should be that you should run `source ~/cs41-env/bin/activate` every time you open a new shell. If you want to get fancy, you can even add this line to your shell startup script (like `~/.bashrc` or `~/.bash_profile`) so it is executed automatically on shell startup.

## What is a virtual environment?
A virtual environment is simply an isolated folder that contains all the executables you need to build something awesome in Python, including code to run the Python interpreter, use [the standard library] (https://docs.python.org/3/library/), and install other third-party libraries that we'll need later in the quarter. Importantly, a virtual environment will keep all of these things in one place (inside the virtual environment folder), so that your local development environment is isolated from the rest of your computer.

## Why bother using virtual environments?
Of course, you could also develop Python projects without a virtual environment, but it's a good idea to become familiar with this tool.

Suppose that you want to use version 2 of the `foo` library but another application requires version 1 of `foo` (this comes up a lot!). How can you have both these applications on your computer at the same time? If you install everything into `/usr/lib/python3.7/site-packages` (or whatever your platform's standard location is), you could easily end up in a sticky situation, in which you might unintentionally upgrade an application that shouldn't be upgraded.

More generally, what if you want to install an application and leave it be? If an application works, any change in its libraries or the versions of those libraries can break the application.

Also, perhaps you can't install packages into the global directory, maybe because you're on a shared host like `rice`. 

In all of these cases, a virtual environment can isolate a project's development and execution environment and make programming in Python a breeze.


## Creating a virtual environment
In Python 3.6+, the recommended way to create a virtual environment is to run:

```
$ python3 -m venv /path/to/new/virtual/environment
```

Make sure that `python3` resolves to whichever version of Python 3 you'd like to bind to your virtual environment.

For example, to create a new virtual environment for CS41 named `cs41-env` in your home folder, you could run:

```
$ python3 -m venv ~/cs41-env
```

## Activation and Deactivation
To activate a virtual environment on macOS or Linux running `bash` or `zsh`, `source` the following path:

```
$ source ~/cs41-env/bin/activate
```

You can replace `~/cs41-env/bin/activate` with the corresponding path if you created your virtual environment in a different location.

If you're using a different shell, you'll need to run a different command:

- `fish`: `$ . ~/cs41-env/bin/activate.fish`
- `csh/tcsh`: `$ source ~/cs41-env/bin/activate.csh`
- `cmd.exe` (Windows): `> ~\cs41-env\Scripts\activate.bat`
- `PowerShell` (Windows): `PS> ~\cs41-env\Scripts\Activate.ps1`

When a virtual environment is activated, you will see a prefix on your prompt, so it will look like this:

```
(cs41-env)$
```

Now that we have an active virtual environment, we can play around with it:

```
(cs41-env)$ python --version
(cs41-env)$ pip --version
(cs41-env)$ python
>>> print("Hello world!")
Hello world!
>>> quit()
(cs41-env)$ 
```

You can create new files, modules, and whatever else you need to make a beautiful Python project!

Most importantly, when a virtual environment is activated, you can install Python packages into this virtual environment using `pip`. For example, to install the numerical Python package `numpy`, run:

```
(cs41-env)$ pip install numpy
```

To deactivate, type

```
(cs41-env)$ deactivate
$
```

That's it!

## Last words and alternatives

To reiterate, **activate your virtual environment every time you open a new shell.**

Also, know that you should not move your virtual environment folder (in the above, that's `~/cs41-env`), as it is subject to break if it is relocated.

There are also some alternatives to virtual environments that operate at a higher level, but are a little more complicated to set up. You can use `virtualenvwrapper` to manage virtual environments in a single place, or the even-higher-level tool `pipenv` to automatically handle everything. You can read more [here](https://docs.python-guide.org/dev/virtualenvs/).

## Credit

Much credit goes to [Python's `venv` documentation](https://docs.python.org/3/library/venv.html) and numerous other online tutorials.


