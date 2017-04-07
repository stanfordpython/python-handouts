# Installing Python 3 with Virtual Environments (Mac/Linux)

In CS41, you'll be writing lots of Python code! Therefore, it's important that you get your development environment ready-to-go as soon as possible.

These instructions are only for Mac OS X and Linux. If you are developing on a Windows computer, see the [Installing Python for Windows](https://docs.google.com/document/d/1tlARF6fipUhwmMru-hdL-avxLrYwPg1KVEIE3L73S48/edit?usp=sharing) setup guide.

## Short Version

1. Install Python 3.4.3
2. Configure `pip`
3. Create a virtual environment
4. Install useful packages

*Disclaimer: These installation instructions have only been tested on Mac OS X - if you find any errors on Linux, please let us know!* 


## Installing Python 3.4.3

Navigate to the [Python 3.4.3 download page](https://www.python.org/downloads/release/python-343/), scroll to the bottom (where it says `Files`) and install the most appropriate distribution of Python.

---
### Mac OS X
If you're running OS X 10.6 or higher, you want the [Mac OS X 64-bit/32-bit installer](https://www.python.org/ftp/python/3.4.3/python-3.4.3-macosx10.6.pkg). After downloading, double-click the downloaded file, and follow the on-screen instructions.

---
### Linux
If you're on Linux, you'll have to build Python from source. Download the source tarball (either [gzipped](https://www.python.org/ftp/python/3.4.3/Python-3.4.3.tgz) or [XZ compressed](https://www.python.org/ftp/python/3.4.3/Python-3.4.3.tar.xz)). Unzip the files and `cd` into the unzipped directory. To build Python, just execute the usual commands:

```
$ ./configure
$ make 
$ make test
$ sudo make install
```

*More information on the Linux installation process can be found in the README included in the tarball.*

---

Let's check to see if Python is installed correctly!

Run the following from a command prompt:

```
$ python3
```

You should see the following:

```
Python 3.4.3 (v3.4.3:9b73f1c3e601, Feb 23 2015, 02:52:03)
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Try writing some Python in the interactive interpreter! When you're done, you can exit the interactive interpreter with CTRL+D or by entering `quit()` at the Python command prompt.

## Getting `pip`

For CS41, we'll be using a package manager called `pip` to install and manage Python software packages. By default, Python 3.4.3 ships with a version of `pip` prebuilt (in our case, `pip3` for Python 3). `pip` interacts very well with PyPI (the Python Package Index), so we'll be using `pip` extensively this quarter.

First, run the following code at a command prompt. You should see something like the sample output (perhaps different for a different OS)

```
$ python3 -m pip --version
pip 7.1.2 from /Library/Frameworks/Python.framework/Versions/3.4/lib/python3.4/site-packages (python 3.4)
```

If it worked, great! If not, check with a member of the course staff before progressing further.

## Configuring Virtual Environment

The following instructions apply to Mac OS X and Linux.

Next, we'll install `virtualenvwrapper`. This third-party software allows for the creation of isolated Python environments, so there is no conflict in the event that you maintain multiple Python installations on your device. You will need to grant root privileges to the installation script (thus the `sudo`), so you may need to enter your password.

Note: `virtualenvwrapper` only works with `bash`, `ksh`, and `zsh`.

```
$ sudo python3 -m pip install virtualenvwrapper
Collecting virtualenvwrapper
  Downloading virtualenvwrapper-4.7.1-py2.py3-none-any.whl
Collecting stevedore (from virtualenvwrapper)
  Downloading stevedore-1.12.0-py2.py3-none-any.whl
Collecting virtualenv (from virtualenvwrapper)
  Downloading virtualenv-15.0.1-py2.py3-none-any.whl (1.8MB)
    100% |████████████████████████████████| 1.8MB 381kB/s
Collecting virtualenv-clone (from virtualenvwrapper)
  Downloading virtualenv-clone-0.2.6.tar.gz
Collecting pbr>=1.6 (from stevedore->virtualenvwrapper)
  Downloading pbr-1.8.1-py2.py3-none-any.whl (89kB)
    100% |████████████████████████████████| 90kB 4.3MB/s
Collecting six>=1.9.0 (from stevedore->virtualenvwrapper)
  Downloading six-1.10.0-py2.py3-none-any.whl
Building wheels for collected packages: virtualenv-clone
  Running setup.py bdist_wheel for virtualenv-clone
  Stored in directory: /Users/<username>/Library/Caches/pip/wheels/<hex_dump>
Successfully built virtualenv-clone
Installing collected packages: pbr, six, stevedore, virtualenv, virtualenv-clone, virtualenvwrapper
Successfully installed pbr-1.8.1 six-1.10.0 stevedore-1.12.0 virtualenv-15.0.1 virtualenv-clone-0.2.6 virtualenvwrapper-4.7.1
```

Next, we'll need to do some one-time setup to configure the virtual environment for this class.

```
$ export WORKON_HOME=$HOME/.virtualenvs
```

This instructs the `virtualenvwrapper` utility to store all of your virtual environments in the folder `.virtualenvs/` in your home directory.

Next, let's see where we installed the `virtualenvwrapper.sh` script.

On a Mac, the easiest way to do this is with `mdfind`, which emulates the behavior of Spotlight.

```
$ mdfind virtualenvwrapper.sh
/Library/Frameworks/Python.framework/Versions/3.4/bin/virtualenvwrapper.sh
/usr/local/bin/virtualenvwrapper.sh
$
```

Copy the first result to your clipboard. If you see no results, or if you see an error like `mdfind: Command not found.`, try the (slower but also effective) command:

```
$ find / -name virtualenvwrapper.sh
< ... lots of output ... >
/Library/Frameworks/Python.framework/Versions/3.4/bin/virtualenvwrapper.sh
/usr/local/bin/virtualenvwrapper.sh
$
```

Copy the first result to your clipboard if you didn't have any luck with `mdfind`.

If there are no results from the `find` command, go back and make sure that you have successfully installed `virtualenvwrapper`. If further problems persist, contact a staff member.

Next, we're going to set up our virtual environment manager:

```
$ source <path/to/virtualenvwrapper.sh>
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/premkproject
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/postmkproject
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/initialize
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/premkvirtualenv
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/postmkvirtualenv
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/prermvirtualenv
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/postrmvirtualenv
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/predeactivate
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/postdeactivate
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/preactivate
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/postactivate
virtualenvwrapper.user_scripts creating /Users/sredmond/.virtualenvs/get_env_details 
```
where `<path/to/virtualenvwrapper.sh>` is the path that you found and copied in the previous step.

For example, you might run `source /Library/Frameworks/Python.framework/Versions/3.4/bin/virtualenvwrapper.sh` or `source /usr/local/bin/virtualenvwrapper.sh`

In order to make sure everything went smoothly, run `workon` from the command prompt. This command prints a list of environments, currently empty.

```
$ workon
$
```

Now, we'll actually create the virtual environment for CS41. You can name your virtual environment anything you want, but we recommend a short, easy-to-remember name. When you run `mkvirtualenv`, a new environment is created, and we specify the particular version of Python to use via the `--python` option.

```
$ mkvirtualenv --python=`which python3` cs41
Running virtualenv with interpreter /usr/local/bin/python3
Using base prefix '/Library/Frameworks/Python.framework/Versions/3.4'
New python executable in cs41/bin/python3
Also creating executable in cs41/bin/python
Installing setuptools, pip, wheel...done.
virtualenvwrapper.user_scripts creating /Users/<username>/.virtualenvs/cs41/bin/predeactivate
virtualenvwrapper.user_scripts creating /Users/<username>/.virtualenvs/cs41/bin/postdeactivate
virtualenvwrapper.user_scripts creating /Users/<username>/.virtualenvs/cs41/bin/preactivate
virtualenvwrapper.user_scripts creating /Users/<username>/.virtualenvs/cs41/bin/postactivate
virtualenvwrapper.user_scripts creating /Users/<username>/.virtualenvs/cs41/bin/get_env_details
```

Now, if you run `workon`, you should see the list of all environments, which now includes `cs41`.

```
(cs41)$ workon
cs41
$
```

### Observations

You may notice that your command prompt now has the name of the active environment, cs41, printed before it. For example, if your old command prompt was

```
sredmond:stanfordpython$ 
```

your new command prompt would be

```
sredmond:stanfordpython$ workon cs41
(cs41)sredmond:stanfordpython$ 
```

If you see this parenthesized environment name, it means that your environment is active. To deactivate the environment, simply run

```
(cs41)$ deactivate
$
```

from a command prompt and you should see the parenthesized environment name disappear.

Let's make sure everything is running smoothly. Run all of the following commands and ensure that the output is appropriate.

```
# Checking `python`
(cs41)$ which python
/Users/<username>/.virtualenvs/cs41/bin/python
(cs41)$ python --version
Python 3.4.3
(cs41)$ python -c "print('Hello world.')"
Hello world.

# Testing `pip`
(cs41)$ which pip
/Users/<username>/.virtualenvs/cs41/bin/pip
(cs41)$ pip --version
pip 7.1.2 from /Users/<username>/.virtualenvs/cs41/lib/python3.4/site-packages (python 3.4)
```

Lastly, we'll install some useful packages that will make development a lot easier.


## Using `pip`: Installing Awesome Packages

Run the following commands. You should see lots of output, but I've omitted it here.
```
(cs41)$ pip install --upgrade pip   # Make sure `pip` is the newest version
(cs41)$ pip install "ipython[all]"  # For ipython interactive interpreter and more
```

Most relevantly, you should now have access to `ipython`, an interactive Python interpreter that is vastly superior to the default Python interpreter. You can read an overview [here](http://ipython.readthedocs.org/en/stable/overview.html) if you'd like. To make sure `ipython` is configured correctly, run it from a command prompt, and ensure that you get something similar to the below.

```
(cs41)$ ipython
Python 3.4.3 (v3.4.3:9b73f1c3e601, Feb 23 2015, 02:52:03)
Type "copyright", "credits" or "license" for more information.

IPython 4.1.2 -- An enhanced Interactive Python.
?         -> Introduction and overview of IPython's features.
%quickref -> Quick reference.
help      -> Python's own help system.
object?   -> Details about 'object', use 'object??' for extra details.

In [1]: 
```

## Important Note
Every time you develop code for CS41, you will need to run `workon cs41` in order to activate your virtual environment. Again, to deactivate it, you can run `deactivate`. It might be convenient to add `workon cs41` to your shell startup script.

On Mac OS X running bash, you can accomplish this with

```
$ echo "export WORKON_HOME=$HOME/.virtualenvs" >> ~/.bash_profile
$ echo "source <path/to/virtualenvwrapper.sh>" >> ~/.bash_profile 
$ echo "workon cs41" >> ~/.bash_profile
```

To see that everything was appended correctly, run

```
$ tail ~/.bash_profile
< ... possibly some other stuff ... >
export WORKON_HOME=/Users/sredmond/.virtualenvs
source /Library/Frameworks/Python.framework/Versions/3.4/bin/virtualenvwrapper.sh
workon cs41
```

or something similar.

If you have a different shell startup script (for example, `~/.profile`), you will need to append the same line to the end of that startup script.

Try opening a new Terminal / iTerm window, and running `workon cs41`, `python`, `ipython`, and `deactivate`.

### Aside: Text Editors

In CS41, we'll be using Sublime Text 3 for development, although Sublime Text 2 will also be fine. You are, of course, free to choose any text editor you please (vim/emacs/nano/xcode/idle/atom/textedit/notepad/etc). On most operating systems, you can provide a default application to open all files of a given type. In our case, you may find it helpful to make every `.py` file open in Sublime Text.

> With <3 by @sredmond
