# Virtual Environments

## What is a virtual environment?
A virtual environment is simply an isolated folder that contains all the executables you need to build something awesome in Python, including code to run the interpreter, use the standard library (https://docs.python.org/2/library/), and install other 3rd-party libraries that we'll touch on towards the end of the quarter. 

## Why bother using virtual environments?
Of course, you can also develop Python projects without a virtual environment, but it's a good idea to become familiar with this tool because you can avoid dependency conflicts between your system-wide Python installations and your project-specific Python installations. For example, if you're using Python to build 3 separate Web apps because you're a beast, Project A might depend on Django version 1.2 while Project C depends on Django version 1.9 (yes, Django is the name of a real Web framework: https://docs.djangoproject.com/en/1.9/releases/). You can create a separate virtual environment for each project then install whichever version you need in each project. When you ship awesome projects later in your Python career, you'll know the exact libraries and versions that your project requires (:

## How to create virtual environment
In class we audibled to using a piece of software called virtualenv to build virtual environments because some people had trouble with the virtualenvwrapper software. After you've installed Python3 and pip (see https://github.com/stanfordpython/python-handouts/blob/master/installing-python.md#linux if you need help with this step), you're almost done. Here's the rest of the commands to execute:

### Install the software (only do this once)
`$ pip install virtualenv`

this uses pip to install the software used to build your virtual environments, called virtualenv

### Creating a virtual environment
cd to your Desktop then execute

`$ virtualenv cs41`

this uses virtualenv to create a new virtual environment in the working directory named cs41. you should be able to see this folder on your Desktop now.

### Activating and deactivating a virtual environment
To activate, simply cd into the environment we created above then execute

`$ source bin/activate`

Now you can play with the interactive interpreter inside your isolated environment using

`$ python3`

You can also create new files, modules, whatever you need to make a beautiful Python project ready to ship!
To deactivate, type

`$ deactivate`

All done! If you want to read more about the above steps, check out http://docs.python-guide.org/en/latest/dev/virtualenvs/

If you want to read about the interactive interpreter, check out http://www.python-course.eu/python3_interactive.php





