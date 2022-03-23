# Installing Python on macOS

Hello!

This document provides a walkthrough to set up a Python development environment for CS 41 on macOS. Alternate versions of this guide exist for [Linux](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-linux.md) and [Windows](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-windows.md) development.

## Overview

In this course, you'll be writing lots of Python code, so it's important to get your development environment set up and ready-to-go. Moreover, we will sometimes need to install dependencies and packages, so we want to make sure that everything gets installed to the right place as well. The tools we learn about in this document will also be useful for any external development you might pursue in Python.

Throughout this document, we will:

1. Install Python 3.10.3
2. Create a virtual environment using this version of Python.
3. Inside this environment, install useful packages.
4. (Optional) Modify the shell startup script to always activate our environment.

Let's get started!

## Install Python 3.10.3

*Note: If you use `brew` or another package manager for Python installations, see the note at the bottom of this section instead.*

Navigate to the [Python 3.10.3 download page](https://www.python.org/downloads/) in a web browser.

Navigate to the top of the page where it says "Looking for Python with a different OS? Python for..." and select your operating system/computer mode.

After downloading, double-click the downloaded file, and follow the on-screen instructions to install Python 3.10.3

Let's double check that Python 3.10.3 was installed correctly.

For the remainder of this setup document, we assume that you have a basic familiarity with the command line. We understand that not everyone will feel comfortable with the command line, because it is usually covered starting in CS107. However, I highly recommend using Nick Troccoli's amazing [CS107 resources](https://web.stanford.edu/class/archive/cs/cs107/cs107.1214/resources/) for this quarter if you feel less experienced, particular the section titled "Common Unix Commands."

The main takeaway is the following: If you something of the following form in this guide (you'll see this quite a few times!):

```
coopermj$ command
```

Then copy and paste the command into your command line prompt. 

Two quick notes:

1. The text before the `$` can vary. It is not necessarily your username. In this case, we are assuming that the username is `coopermj` and that is the text which is shown before the `$` at your command prompt. (On the terminal below, for example, the text before the prompt includes more than just the username, including the current directory).
2. Below is a quick example of how you may go about running the commands immediately following this list. This is designed to clear up any ambiguity related to running commands at the command line. 

![](term_example.png)

Open up a command line prompt (likely using Terminal), and run the following commands:

```
coopermj$ which python3
/Library/Frameworks/Python.framework/Versions/3.9/bin/python3
coopermj$ python3 --version
Python 3.9.2
```

If you see the output shown above, then Python 3.9.2 was installed correctly on your machine!

Let's celebrate by writing some code! Run the following from a command prompt. You should see the following output, which leaves you at an interactive prompt, at which you can write Python code.

```
coopermj$ python3
Python 3.9.2 (v3.9.2:1a79785e3e, Feb 19 2021, 09:06:10) 
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello world!")
Hello world!
>>> quit()
coopermj$ 
```

Try writing some Python (perhaps `print("Hello world!")`) in the interactive interpreter! When you're done, you can exit the interactive interpreter by entering `quit()` at the Python command prompt or by pressing CTRL+D.

#### Other package managers: `brew`

[Homebrew](https://brew.sh/) is "the missing package manager for macOS." It's a great way to install, upgrade, and manage many different types of packages on macOS, including Python. If you are not using `brew`, there is no requirement that you start for CS41. However, if you are already using `brew`, you might as well install Python through brew.

Run `brew install python3`. This will fetch the latest version of Python (which might not be Python 3.9.2, but that's all we can do).

Then, continue the process above, after the installation of Python 3.9.2.

### Troubleshooting

#### `which python3` shows no output
The `which` command searches your computer for a program matching a name. If `which python3` shows no output, it means that your computer can't find any appropriate `python3`. Pause and reach out to a member of the course staff to help you debug. Include as much detail as you can about the problem.

#### `python3 --version` does not show `Python 3.9.2`
In this case, the version of Python 3 your computer wants to run is not the Python 3.9.2 that we just downloaded. Pause and reach out to a member of the course staff to help you debug. Include as much detail as you can about the problem.

## Create a virtual environment

We've correctly installed Python, so next we will create a virtual environment. You can learn more about virtual environments [here](https://github.com/stanfordpython/python-handouts/blob/master/virtual-environments.md) or at the end of our [lecture slides](https://stanfordpython.com/#lectures) on Python fundamentals, but for now it is sufficient to think of a virtual environment as an isolated sandbox for Python packages and dependencies.

Specifically, we will create a folder named `cs41-env` in your computer's home folder. The configuration of our virtual environment will live entirely inside of this folder.

```
coopermj$ python3 --version
Python 3.9.2
coopermj$ python3 -m venv ~/cs41-env
```

If these two lines execute without error, you have successfully created a virtual environment named `cs41-env`.

*Note: If you move the `cs41-env` folder, some of the internal structure of the virtual environment can break in unpredictable ways. This is one of the drawbacks of standard virtual environments that motivate our more advanced usage of `virtualenvwrapper` later in this document.*

### Activating a virtual environment

For a given terminal session, a virtual environment is either active or inactive at any moment in time. To activate our virtual environment, you will need to run

```
coopermj$ source ~/cs41-env/bin/activate
(cs41-env) coopermj$
```

*Note: If your shell is `tcsh` or `csh`, you will have to run `source ~/cs41-env/bin/activate.csh` instead. If your shell is `fish`, you will have to run `. ~/cs41-env/bin/activate.fish` instead.*

Observe that our command prompt, which previously was `coopermj$`, now is `(cs41-env) coopermj$`. This is one method by which you can see whether a virtual environment is activated.

### Deactivating a virtual environment

Deactivating a virtual environment is easy. From an activated environment, simply run

```
(cs41-env) coopermj$ deactivate
coopermj$
```

Don't worry if you deactivate from an inactive environment. Nothing bad will happen, although you might see a `-bash: deactivate: command not found` error message, which you can safely ignore.

### Using an activated virtual environment.

Let's reactivate our virtual environment to see what's different when a virtual environment is active.

```
coopermj$ source ~/cs41-env/bin/activate
(cs41-env) coopermj$ which python3
/Users/coopermj/cs41-env/bin/python3
(cs41-env) coopermj$ which python
/Users/coopermj/cs41-env/bin/python
(cs41-env) coopermj$ which pip3
/Users/coopermj/cs41-env/bin/pip3
(cs41-env) coopermj$ which pip
/Users/coopermj/cs41-env/bin/pip
```

It looks like all of our python-related commands are now located inside of the virtual environment. That's a good thing! You can confirm this by seeing that `/Users/coopermj/cs41-env/bin:` is the first entry of the string printed by running `echo $PATH`.

Moreover, observe that:

```
(cs41-env) coopermj$ python3 --version
Python 3.9.2
(cs41-env) coopermj$ python --version
Python 3.9.2
(cs41-env) coopermj$ pip3 --version
pip 21.0.1 from /Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages/pip (python 3.9)
(cs41-env) coopermj$ pip --version
pip 21.0.1 from /Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages/pip (python 3.9)
```

The big takeaway is that, inside our active virtual environment, the commands `python` and `pip` now refer to Python 3.9.2 and it's associated package manager.

For example, when the virtual environment is active, we can enter an interactive Python 3 prompt simply by running:

```
coopermj$ python
Python 3.9.2 (v3.9.2:1a79785e3e, Feb 19 2021, 09:06:10) 
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

*As a reminder, you can quit the interactive Python prompt with `quit()` or CTRL+D.*

## Use `pip` to Install Useful Packages

Next, we'll install useful Python packages that will serve us over the duration of this course. Let's first make sure that we're have activated the virtual environment.

```
coopermj$ source ~/cs41-env/bin/activate
```

Now, we'll update `pip`, Python's builtin package manager, just to make sure it's on the latest version (it should be).

```
(cs41-env) coopermj$ pip install --upgrade pip
Requirement already up-to-date: pip in ./cs41-env/lib/python3.9/site-packages (21.0.1)
```

After, we'll install the suite of Jupyter tools and some additional useful packages.

*Really, really make sure that you have activated `cs41-env` before running this line!*

```
(cs41-env) coopermj$ pip install "prompt-toolkit==2.0.10" "ipython[all]" jupyter jupyterlab numpy scipy matplotlib nltk scikit-learn requests flask pycodestyle autopep8 Pillow
```

This will produce a huge amount of output, as Python is downloading these third-party libraries and tools from the internet and storing them inside our virtual environment. These packages will be available when our virtual environment is active, but will not necessarily be available if our virtual environment is inactive. For this reason, it's important to always have an active virtual environment when working on code for this class.

The last few lines of the output should look like the following. If your output is dramatically different from this or the installation failed with an error, pause and get a member of the course staff to help or post on Piazza.

```
Installing collected packages: wcwidth, prompt-toolkit, appnope, ptyprocess, pexpect, parso, jedi, pickleshare, pygments, ipython-genutils, traitlets, decorator, backcall, pytz, babel, sphinxcontrib-serializinghtml, snowballstemmer, urllib3, idna, certifi, chardet, requests, packaging, docutils, sphinxcontrib-jsmath, sphinxcontrib-devhelp, sphinxcontrib-qthelp, imagesize, sphinxcontrib-applehelp, MarkupSafe, jinja2, alabaster, sphinxcontrib-htmlhelp, Sphinx, entrypoints, pandocfilters, jupyterlab-pygments, testpath, mistune, webencodings, bleach, jupyter-core, attrs, pyrsistent, jsonschema, nbformat, defusedxml, pyzmq, tornado, jupyter-client, nest-asyncio, async-generator, nbclient, nbconvert, nose, pycparser, cffi, argon2-cffi, Send2Trash, terminado, ipykernel, prometheus-client, notebook, widgetsnbextension, jupyterlab-widgets, ipywidgets, qtpy, qtconsole, ipyparallel, ipython, jupyter-console, jupyter, sniffio, anyio, jupyter-server, nbclassic, jupyter-packaging, json5, jupyterlab-server, jupyterlab, scipy, click, joblib, regex, tqdm, nltk, threadpoolctl, scikit-learn, Werkzeug, itsdangerous, flask, toml, autopep8
    Running setup.py install for pandocfilters ... done
    Running setup.py install for pyrsistent ... done
    Running setup.py install for nltk ... done
Successfully installed MarkupSafe-1.1.1 Send2Trash-1.5.0 Sphinx-3.5.3 Werkzeug-1.0.1 alabaster-0.7.12 anyio-2.2.0 appnope-0.1.2 argon2-cffi-20.1.0 async-generator-1.10 attrs-20.3.0 autopep8-1.5.6 babel-2.9.0 backcall-0.2.0 bleach-3.3.0 certifi-2020.12.5 cffi-1.14.5 chardet-4.0.0 click-7.1.2 decorator-4.4.2 defusedxml-0.7.1 docutils-0.16 entrypoints-0.3 flask-1.1.2 idna-2.10 imagesize-1.2.0 ipykernel-5.5.0 ipyparallel-6.3.0 ipython-7.22.0 ipython-genutils-0.2.0 ipywidgets-7.6.3 itsdangerous-1.1.0 jedi-0.18.0 jinja2-2.11.3 joblib-1.0.1 json5-0.9.5 jsonschema-3.2.0 jupyter-1.0.0 jupyter-client-6.1.12 jupyter-console-6.4.0 jupyter-core-4.7.1 jupyter-packaging-0.7.12 jupyter-server-1.5.1 jupyterlab-3.0.12 jupyterlab-pygments-0.1.2 jupyterlab-server-2.3.0 jupyterlab-widgets-1.0.0 mistune-0.8.4 nbclassic-0.2.6 nbclient-0.5.3 nbconvert-6.0.7 nbformat-5.1.2 nest-asyncio-1.5.1 nltk-3.5 nose-1.3.7 notebook-6.3.0 packaging-20.9 pandocfilters-1.4.3 parso-0.8.1 pexpect-4.8.0 pickleshare-0.7.5 prometheus-client-0.9.0 prompt-toolkit-2.0.10 ptyprocess-0.7.0 pycparser-2.20 pygments-2.8.1 pyrsistent-0.17.3 pytz-2021.1 pyzmq-22.0.3 qtconsole-5.0.3 qtpy-1.9.0 regex-2021.3.17 requests-2.25.1 scikit-learn-0.24.1 scipy-1.6.2 sniffio-1.2.0 snowballstemmer-2.1.0 sphinxcontrib-applehelp-1.0.2 sphinxcontrib-devhelp-1.0.2 sphinxcontrib-htmlhelp-1.0.3 sphinxcontrib-jsmath-1.0.1 sphinxcontrib-qthelp-1.0.3 sphinxcontrib-serializinghtml-1.1.4 terminado-0.9.3 testpath-0.4.4 threadpoolctl-2.1.0 toml-0.10.2 tornado-6.1 tqdm-4.59.0 traitlets-5.0.5 urllib3-1.26.4 wcwidth-0.2.5 webencodings-0.5.1 widgetsnbextension-3.5.1
```

We will learn more about each of these packages throughout this course.

Importantly, you should now have access to `ipython`, an interactive Python interpreter that is (in our humble opinion) vastly superior to the default Python interpreter. You can read an overview [here](http://ipython.readthedocs.org/en/stable/overview.html) if you'd like. To make sure `ipython` is configured correctly, run it from a command prompt, and ensure that you get something similar to the below.

```
(cs41-env)$ ipython
Python 3.9.2 (v3.9.2:1a79785e3e, Feb 19 2021, 09:06:10) 
Type 'copyright', 'credits' or 'license' for more information
IPython 7.22.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]:
```

One helpful feature of `ipython` is that you can append a `'?'` to any symbol and Python will try to give you help for that symbol. For example:

```
In [1]: print?
Docstring:
print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)

Prints the values to a stream, or to sys.stdout by default.
Optional keyword arguments:
file:  a file-like object (stream); defaults to the current sys.stdout.
sep:   string inserted between values, default a space.
end:   string appended after the last value, default a newline.
flush: whether to forcibly flush the stream.
Type:      builtin_function_or_method
```

And that's it! You are all done setting up your Python development environment for CS41.

## Summary

First, we installed Python 3.9.2 from the Python website and checked that everything was installed correctly. Next, we used `python3` to create a virtual environment named `cs41-env`, and we learned how to activate and deactivate this virtual environment. Lastly, we activated the environment and installed lots of useful packages.

**Reminder: Each time you create a new terminal session, you will need to run `source ~/cs41-env/bin/activate`.**

## IMPORTANT! Activating virtual environments

One very important note is that our virtual environment will not be activated by default. This means that, for every new command line session you create (for example, by opening a new tab in Terminal.app or iTerm.app), you will need to run `source ~/cs41-env/bin/activate` to activate the `cs41-env` virtual environment. A good rule to remember is: if you don't see `(cs41-env)` at the start of the command prompt, then the virtual environment is not active!

In this course, we always assume that you are operating in an active virtual environment. So, it's crucially important that you activate the `cs41-env` environment by running `source ~/cs41-env/bin/activate` in every terminal session you use for this class.

### Optional: Automatically enable `cs41-env`

If you want to automatically enable the `cs41-env` virtual environment every time you start a new interactive session, you can add a command to your shell's startup script. In most cases, this will be `~/.bash_profile` or `~/.bashrc`, which are different but in ways that are not important to us right now. Run:

```
coopermj$ echo "# Activate virtual environment for CS41." >> ~/.bash_profile
coopermj$ echo "source ~/cs41-env/bin/activate" >> ~/.bash_profile
coopermj$ tail -n 2 ~/.bash_profile
# Activate virtual environment for CS41.
source ~/cs41-env/bin/activate
```

This will cause the command `source ~/cs41-env/bin/activate` to be executed every time you open a new terminal session. Since this script gets executed every time you create a new terminal session, the `cs41-env` will be automatically activated. It can still be deactivated by running `deactivate`.

*Note: If you are using a different shell (`tcsh`, `zsh`, etc) than `bash`, you will need to place this startup command in your appropriate startup script, such as `~/.tcshrc` or `~/.zshrc`.*

You did it! Celebrate with your friends.

## Credit
Much of this handout was based on a similar handout written by Sam Redmond (@samredmond)
