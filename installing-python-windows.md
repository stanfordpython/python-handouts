# Installing Python on Windows

We provide three strategies for setting up a Python environment on windows.

1. Bash on Ubuntu on Windows
2. Running Directly on Windows
3. Using a VM

We recommend Strategy 1, as it will give you a development environment that is similar enough to the macOS and Linux instructions that you will be able to act almost as if you have a Linux computer.

We discourage Strategy 2, as it is the most complicated and hardest for us to debug.

We are fine with Strategy 3, although it is essentially just avoiding the problem by throwing computational resources at it.

If Strategy 1 or Strategy 2 fail horribly, Strategy 3 will definitely work, but is fairly resource intensive.

So, we recommend trying out Strategy 1 first. If that fails, decide whether you are willing to allocate a nontrivial amount of computing resources to this course. If so, proceed with Strategy 3. If not, proceed with Strategy 2.

## (1) Bash on Ubuntu on Windows
Requires: 64-bit Windows 10, updated to the 2016 Anniversary build or later. *If you regularly download updates, you'll be fine.*

Windows 10 has added a Ubuntu subsystem which we will use for development in this class. In particular, we'll use the Ubuntu system to download Python and to create a virtual environment for this course.

First, follow [these instructions](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) from HowToGeek in order to activate the "Windows Subsystem for Linux," get Ubuntu from the Microsoft Store, and launch a `bash` shell on Ubuntu.

One quick note here: Your Windows file system is located at `/mnt/c` in the Bash shell environment.

Once you're in the `bash` shell, you can follow the [Linux](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-linux.md) guide, which has more details. If you're just getting started, you may also need to run the following commands:

```
$ sudo add-apt-repository ppa:deadsnakes/ppa
$ sudo apt-get update
$ sudo apt-get install python3.8
$ sudo apt-get install python3.8-venv
```

You can check which version of Python you've installed by running:

```
$ python3 --version
Python 3.8.0
```

In broad strokes, you will need to run the following commands to set up a virtual environment. The Linux and macOS handouts contain more detailed information.

```
$ python3 -m venv "${HOME}/cs41-env"
$ source "${HOME}/cs41-env/bin/activate"
(cs41-env)$ pip install "ipython[all]" jupyter jupyterlab numpy scipy matplotlib nltk scikit-learn requests flask pycodestyle autopep8 Pillow
(cs41-env)$ deactivate
```

The command `source "${HOME}/cs41-env/bin/activate"` is especially important. **Every time you open a new bash shell, you will need to run `source "${HOME}/cs41-env/bin/activate"` in order to activate your virtual environment.** The `deactivate` command deactivates an active virtual environment.

You can tell if a virtual environment is active by looking for the parenthesized `(cs41-env)` prefix.

Working with Windows is complicated enough, so we're going to omit the instructions for how to use `virtualenvwrapper` to set up managed virtual environments. If you're really interested, you can follow the macOS instructions for `virtualenvwrapper`.

## (2) Running Directly on Windows

Recall that we discourage this option as it is very complex and hard for us to debug. Only use this option if the above fails and you don't want to use a VM (Strategy 3) for some reason.

You will need Windows Vista or newer to use Python 3.8.0 on Windows.

When in doubt, the source of truth for Windows commands is [included in the Python documentation](https://docs.python.org/3/using/windows.html), and you can find more details on using virtual environments [here](https://docs.python.org/3/library/venv.html#module-venv).

The rough outline is:

1. Install Python 3 and sanity check the installation.
2. Create a virtual environment.
3. Use `pip` to install useful packages.

First, download the web-based installer from the [Python 3.8.0 releases page](https://www.python.org/downloads/release/python-380/), either for [x86-64](https://www.python.org/ftp/python/3.8.0/python-3.8.0-amd64-webinstall.exe) or [x86](https://www.python.org/ftp/python/3.8.0/python-3.8.0-webinstall.exe). The web-based installer is a small download which will connect to the internet to download any additional required components, so make sure that you are connected to the internet for the remainder of these installation instructions.

Start the installer. You will see two options: "Install launcher for all users (recommended)" and "Add Python 3.8 to PATH". Make sure both are selected, and then click "Install Now."

*Note: Technically, you should also [remove the MAX_PATH limitation](https://docs.python.org/3/using/windows.html#removing-the-max-path-limitation), but we'll skip that for now.*

Follow the on-screen instructions to finish installing Python. When you are given the option of unchecking any 'optional' components, do not uncheck any. In particular, if there is an option called "Add python.exe to search path" on the "Customize Python 3.8" screen, make sure that box is checked! You should also see that `pip` is being installed by default.

Let's check to see that everything was installed correctly.

Open up PowerShell or `cmd.exe` and run the following from a command prompt:

```
> python3
```

You should see something like the following:

```
Python 3.8.0 (v3.8.0:fa919fdf25, Oct 14 2019, 10:23:27)
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Ensure that the Python version above looks like 3.7.2.

If that doesn't work, try running:

```
> python
```

If this drops you into a Python 3.8.0 interactive interpreter, great! In this case, everywhere you see `python3` below, replace it with the command `python`.

If this didn't work, try running:

```
> py -3
```

If this worked, then everywhere you see `python3` below, replace it with the command `py -3`.

Try writing some Python in the interactive interpreter! When you're done, you can exit the interactive interpreter with `CTRL+C` or by entering `quit()` at the Python command prompt.

### Checking `pip`
First, let's check that we have `pip` installed. For CS41, we'll be using a package manager called `pip` to install and manage Python software packages. By default, Python 3.8.0 ships with a version of `pip` prebuilt. `pip` interacts very well with PyPI (the Python Package Index), so we'll be using `pip` extensively this quarter.

At a command prompt, run the following code. You should see something like the following output:

```
> python3 -m pip --version
pip 19.3 from /pip 19.3 from C:\Users\Parth\AppData\Local\Programs\Python\Python38\lib\site-packages (python 3.8)
```

Problems might arise if you had a different version of Python 3 already installed, but if you added Python 3.8 to your PATH, this should work.

### Create a Virtual Environment

Great! Now, let's run the following commands:

```
> python3 -m venv ~\cs41-env
```

If you were having trouble with finding your Python executable in the previous section, you should be able to instead run the following, in which you specify the full path to all arguments:

```
c:\> c:\Python38\python -m venv c:\path\to\myenv
```

This will create a virtual environment in a folder named `cs41-env` inside your home folder.

To activate the virtual environment, you must run one of the following two commands. If you are using `cmd.exe`, you must run:

```
C:\> ~\cs41-env\Scripts\activate.bat
```

If you are using PowerShell, you should run:

```
PS C:\> ~\cs41-env\Scripts\Activate.ps1
```

As with other OSes, you can deactivate the virtual environment by running `deactivate` in your shell.

### Installing packages with `pip`

Go ahead and activate your virtual environment, using the appropriate command above for either `cmd.exe` or PowerShell. Next, install the following packages into your virtual environment using `pip`:

```
(cs41-env) > pip install "ipython[all]" jupyter jupyterlab numpy scipy matplotlib nltk scikit-learn requests flask pycodestyle autopep8 Pillow
```

When you're done with that, `deactivate` the virtual environment.

You're all set! Give yourself a pat on the back. Remember that every time you open a new shell, you will need to activate your virtual environment.

## (3) Use a Virtual Machine

It can be very hard to properly set up development environments on Windows. We're going to give up on Windows, and instead we'll use VirtualBox to run an entire Linux operating system on your Windows computer. First, [download VirtualBox 6.1.0](https://download.virtualbox.org/virtualbox/6.1.0/VirtualBox-6.1.0-135406-Win.exe). Make sure you know where you have downloaded this file.

Great! We're halfway there.

Next, you'll need to download a Unix OS. We recommend using [Ubuntu 18.04](https://www.ubuntu.com/download/desktop/thank-you?version=18.04.1&architecture=amd64). Now, 

1. Launch VirtualBox by double-clicking on the downloaded executable.
2. Create a new VM instance and point the prompt to the Ubuntu ISO you just downloaded.
3. VirtualBox will prompt you to configure lots of settings for your new virtual machine. You can use the defaults, or you can adjust the settings if you know what you are doing. Roughly speaking, the more resources you give to your VM, the fewer your normal non-VM computer has.
	a. You can name your virtual machine something like `cs41-vm` 
4. Click through the on-screen instructions to finish setting up Ubuntu.

Ubuntu is a Linux distribution, so from here you should follow the [Linux](https://github.com/stanfordpython/python-handouts/blob/master/installing-python-linux.md) guide that has already been posted.

If you'd like to be oriented to VirtualBox itself, they have posted [a manual](https://www.virtualbox.org/manual/ch01.html) (warning: it's pretty long) that covers First Steps with VirtualBox. If you only read one section, we recommend "Section 1.9: Running Your Virtual Machine."

# Credit
Much of this handout was based on a similar handout written by Sam Redmond (@samredmond)
