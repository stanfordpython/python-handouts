# CS41 Submission Instructions

At a high level, submitting code for CS41 consists of 2 major parts.

1. Upload your files to Stanford's AFS server
2. Submit your program using `/usr/class/cs41/tools/submit`

Easy, right? Let's chat in more detail.

If you've already taken CS107 and feel comfortable with Unix, skip to the section titled "Upload Files to Myth."

*In all of the below examples, content inside angle braces (`<sunet>`) should be replaced with the correct information.*

## Background Information

### Overview

Everything we'll do this quarter involves running commands on Unix. Developed in the 70s at Bell Labs, Unix is an operating system, like Windows, Android or MacOS. Over the years, Unix and its derivatives and cousins, including Linux, have become ubiquitous. In fact, MacOS X is built on Unix and lets you access its Unix insides through the Terminal (more on that later). Although technically Linux (that we'll use in this class) isn't Unix, but rather a copy-cat of Unix rebuilt from the ground up to address some of Unix's limitations. However, the interface that users (that's us!) see is so similar that for the purposes of this class "Linux" and "Unix" are synonymous.

In CS41, we'll be submitting assignments on "myth," a cluster of computers in the basement of Gates running Ubuntu Linux. The myth computers themselves are physically located in Gates B08. You can also use them remotely to do assignments, because the room is not always available to everyone.

### Logging into `myth` with SSH

The first step of this assignment is to set up your own computer to log in to myth. Logging in through a program called ssh will allow you to work on the myth computers in a way that is indistinguishable from being physically in the Gates B08 room. While some version of ssh is available on all kinds of computers, the exact details of this step will be different depending on what kind of computer you have:

- [MacOS](https://web.stanford.edu/class/cs107/assign0/macos.html): Use this if you have your own Mac or you are on a Stanford lab machine in libraries, dorms, etc.
- [Windows](https://web.stanford.edu/class/cs107/assign0/windows.html): Use this if you have a Windows computer.
- [Linux](https://web.stanford.edu/class/cs107/assign0/linux.html): Use this if you have a Linux computer.

Do not proceed until you have seen `myth`'s successful login welcome text, as shown at the links above.

### Upload/Downloading Files with FTP/SCP

The above instructions allow you to access `myth` to do things on `myth` - edit your code, run your code, debug your code, submit your code, and so on. What it doesn't allow you to do is to bring any files that are on `myth` back with you to your own computer. To do that, you'll need an FTP/SCP file transfer program. There are several options for this, again varying based on your operating system. But one reliable approach is probably just to use [Stanford's AFS web interface](https://afs.stanford.edu). You'll be asked to log in to Stanford as you would for Axess and other secure Stanford websites (unless you are already logged in to one of those at the moment). It will then take you to a list of all the files on your myth account. Click the download icon next to any file to download it. You can also upload files using this web interface, and files you add will be visible when you ssh to myth.

## Upload Files to Myth

**TL:DR**

```
$ ssh <sunetid>@myth.stanford.edu "mkdir -p ~/cs41/assign{0,1,2,3,4}"
$ scp -r <path/to/assignment/directory> <sunetid>@myth.stanford.edu:~/cs41/
```

*Note: you should replace every instance of `<sunetid>` with your own SUNetID.*

### Create Folder Structure on AFS

First, you can optionally construct a folder for your submission to land in - we suggest `~/cs41/`. 

If you're on a Macintosh or Linux computer, you can run

```
$ ssh <sunetid>@myth.stanford.edu "mkdir -p ~/cs41/assign{0,1,2,3,4}"
```

It may ask for your password, in which case you should type in your Stanford (SUNet) password. Don't worry if it doesn't appear as you type it - it's not supposed to!

If you're on a Windows computer, you can use a graphical interface ([SecureFX](https://uit.stanford.edu/software/securefx), [FileZilla](https://filezilla-project.org/), [Fugu](http://rsug.itd.umich.edu/software/fugu/)) or a specialized Unix-ish terminal ([cmder](http://cmder.net/), [powershell](https://msdn.microsoft.com/en-us/powershell/scripting/setup/installing-windows-powershell), [MobaXterm](http://mobaxterm.mobatek.net/)) to accomplish this task, but you can *also* do it with the [AFS web client](https://afs.stanford.edu)! Hooray!

Go to [afs.stanford.edu](https://afs.stanford.edu) and click "Create a New Folder" on the left hand side. Name the new folder `cs41`! Inside this folder, create five new folders:

```
assign0/
assign1/
assign2/
assign3/
assign4/
```

When done, you should see something like this:
![AFS Structure](https://raw.githubusercontent.com/stanfordpython/python-handouts/master/img/afs-structure.png)

### Upload files to AFS

On Mac/Linux, you need to copy your files over to the FarmShare servers. You can do this via 

```
$ scp -r <path/to/assignment/directory> <sunetid>@myth.stanford.edu:~/cs41/
```

where `<path/to/assignment/directory>` is a filepath identifying the directory your solution code is in, and `<sunetid>` is your SUNetID.

On Windows, if you have an `scp` tool, you can do the same thing. Otherwise, you can use one of the GUI programs or specialized terminals (described at the start of this file) or just upload your files manually via the [WebAFS client](https://afs.stanford.edu).

## Submitting Code!

**TL:DR**

```
$ ssh <sunetid>@myth.stanford.edu
myth$ cd ~/cs41/<assignment_folder>/
myth$ /usr/class/cs41/tools/sanitycheck ./
myth$ /usr/class/cs41/tools/submit ./
```

We providing both a `sanitycheck` tool and a `submit` tool.

If you're on Windows, you'll need to SSH into Stanford FarmShare (`myth`, `corn`, etc.). Hopefully, you already know how to do this, but if not, University IT has some [good solutions](https://uit.stanford.edu/service/sharedcomputing/loggingin), if the earlier SSH solutions didn't work.

### sanitycheck

The `sanitycheck` script, in general, will exercise some basic functionality of your assignment. It isn't extensive, and we'll be testing your code on more advanced test cases, but it should provide you with some confidence that everything is at least set up correctly and working properly on basic inputs.

When logged into myth (or another of the Stanford computer clusters), first navigate to your submission directory. From there, you test your code by running

```
myth$ /usr/class/cs41/tools/sanitycheck ./
```

### submit

When you're ready to submit, make sure that you're currently in your submission directory (you can check by running `pwd` on myth), and run

```
myth$ /usr/class/cs41/tools/submit
```

You should get output that looks something like:

```
Hello, sredmond
Which assignment are you submitting?
* Please enter the assignment number
0: Welcome to Python
1: Cryptography
2: Quest for the Holy Grail
3: Stylize
4: Final Project
> 0
Submission for Assignment #0
This isn't a question - but it's the last step... I'm about to upload all files in the current folder to AFS. Hit ENTER to confirm this is desired.
```

Note that you have the option to run sanity check before submitting.

## Notes

There are a few important things to consider:

1. Every time that you want to submit a new version of your assignment, you must upload your changed files to AFS (myth), and run `/usr/class/cs41/tools/submit`
2. We'll grade the most recent assignment that you submit.
3. Make sure that you're running the `tools` scripts from inside your assignment directory! Otherwise there might be some weird errors.

## Credit

Several sections of this handout were copied, verbatim, from Cynthia's incredible [CS107 introductory materials](https://web.stanford.edu/class/cs107/assign0/), and some instructive commands (especially for SCPing from Windows) came from [CS221's submission instructions](http://web.stanford.edu/class/cs221/). It wouldn't be possible without them!