# Installing A Virtual Environment (Mac OS X and Linux)

Hi there!

This is a quick tutorial on how to set up pip and virtual environments on your local computer. These are crucial to have at the beginning of the quarter so you are able to install the appropriate dependencies and packages into your computer and also properly install them in the right places. Along with this, these are genuinely useful (& arguably necessary) for any external Python development that you will pursue. So, what are they?

## Pip
Pip is a package management system used to install and manage software packages written in Python. You will most likely use pip to install most of your dependencies for your projects. To install pip on your system, open up your terminal, and type in and enter:

```
sudo easy_install pip
```

This will prompt your terminal to ask you for your system password, enter it, and then pip should be installed on your computer. To install any package on your computer globally, just use:

```
pip install some-package-name
```

You can easily remove the package by using: 

```
pip uninstall some-package-name
```

But, before you install any more packages globally, let's talk about virtual environments. 

## Virtual Environments
A Virtual Environment is a tool to keep the dependencies required by different projects in separate places, by creating virtual Python environments for them. It solves the "Project X depends on version 1.x but, Project Y needs 4.x" dilemma, and keeps your global site-packages directory clean and manageable.

What does this mean? Well, when you install different libraries and software packages, you are constantly installing specific versions of those packages. If you install it straight on your terminal (globally) without a virtual environment, then your global system will have specific versions that might conflict with a project you might have that might require another version of the same package. 

What do Virtual Environments do? They create folders that contain all the necessary executabels to use the packages that a Python project would need (yes, they are just normal folders found in either Finder or terminal). Virtualenv is a tool to create such isolated Python environments. 

Install virtualenv via pip:

```
$ pip install virtualenv
```

Basic Usage
1. Create a virtual environment for a project:

```
$ cd my_project_folder 
$ virtualenv my_project
```

`virtualenv my_project` will create a folder in the current directory which will contain the Python executable files, and a copy of the pip library which you can use to install other packages. The name of the virtual environment (in this case, it was `my_project`) can be anything; omitting the name will place the files in the current directory instead. 

This creates a copy of Python in whichever directory you ran the command in, placing it in a folder named `my_project`. 

You can also use the Python interpreter of your choice (like python3)

```
$ virtualenv -p </path/to/python3> my_project
```

2. To begin using the virtual environment, it needs to be activated:

```
$ source my_project/bin/activate
```

The name of the current virtual environment will now appear on the left of the prompt to let you know that it's active. From now on, any package that you install using pip will be placed in the my_project folder, isolated fromt he global Python installation. 
Install packages as usual, for example

```
$ pip install requests
```
3. If you are done working in the virtual environment for the moment, you can deactivate it:

```
$ deactivate
```

This puts you back to the system's default Python interpreter with all its installed libraries. To delete a virtual environment, just delete its folder.  

## Virtual Environment Wrappers
Next, we'll install virtual environment wrappers. `virtualenvwrapper` provides a set of commands which makes working with virtual environments much more pleasant. It also places all your virtual environments in one place.

To install (make sure you do this AFTER virtualenv is already installed):

```
$ pip install virtualenvwrapper
$ export WORKON_HOME=$HOME/.virtualenvs
$ source /usr/local/bin/virtualenvwrapper.sh
```

Make sure the third line is the correct path to the virtualenvwrapper.sh on your computer. Run a simple "find" command or search within your Finder if you are not sure what the path is!

### Shell Startup File
Add three lines to your shell startup file (.bashrc, .profile, etc.) to set the location where the virtual environments should live, the location of your development project directories, and the location of the script installed with this package:

```
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Devel
source /Library/Frameworks/Python.framework/Versions/2.7/bin/virtualenvwrapper.sh
```

To make sure that your .bashrc looks like the above, run this command in your terminal: vim ~/.bashrc
After editing it, reload the startup file (e.g., run source ~/.bashrc in your terminal window).

virtualenvwrapper Quick-Start
1. Run: `workon`
2. A list of environments, empty, is printed.
3. Run: `mkvirtualenv cs41`
4. A new environment, `cs41` is created and activated.
5. Run: `workon`
6. This time, the temp environment is included.

References:
- [The Hitchhiker's Guide to Python](http://python-guide-pt-br.readthedocs.io/en/latest/dev/virtualenvs/)
- [Pip (package manager)](https://en.wikipedia.org/wiki/Pip_(package_manager))
