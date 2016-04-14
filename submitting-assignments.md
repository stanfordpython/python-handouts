# CS41 Submission Instructions

At a high level, submitting code for CS41 consists of 2 major parts.

1. Upload your files to Stanford's AFS server
2. Submit your program using `/usr/class/cs41/tools/submit`

Easy, right? Let's chat in more detail.

## Upload Files to Myth

**TL:DR**

```
$ ssh <sunetid>@myth.stanford.edu "mkdir -p ~/cs41/"
$ scp -r <~/path/to/assign1> <sunetid>@myth.stanford.edu:~/cs41/
```

*Note: you should replace every instance of `<sunetid>` with your own SUNetID.*

### Create Folder Structure on AFS

First, you can optionally construct a folder for your submission to land in - we suggest `~/cs41/`. 

If you're on a Macintosh or Linux workstation, you can run

```
$ ssh <sunetid>@myth.stanford.edu "mkdir -p ~/cs41/"
```

It may ask for your password, in which case you should type in your Stanford password. Don't worry if it doesn't appear - it's not supposed to!

If you're on a Windows computer, you can use any number of tools (powershell, MobaXterm, etc) to accomplish this task, but you can *also* do it with a web client! Hooray!

Go to [afs.stanford.edu](afs.stanford.edu) and click "Create a New Folder" on the left hand side. Name the new folder `cs41`!

### Upload files to AFS

On Mac/Linux, you need to copy your files over to the FarmShare servers. You can do this via 

```
$ scp -r <~/path/to/assign1> <sunetid>@myth.stanford.edu:~/cs41/
```

where `<~/path/to/assign1>` is a filepath identifying the directory your solution code is in, and `<sunetid>` is your SUNetID. For example, for me this line would be `$ scp -r ~/stanfordpython/python-assignments/assign1 sredmond@myth.stanford.edu:~/cs41`

On Windows, if you have an `scp` tool, you can do the same thing. Otherwise, you can use a 3rd party solution (like MobaXterm!) or just upload your files manually via the WebAFS client (at afs.stanford.edu). For this assignment, you'll only need to upload `crypto.py`, `utils.py`, `design.txt`, and `feedback.txt`.

## Submitting Code!

**TL:DR**

```
$ ssh <sunetid>@myth.stanford.edu
myth$ cd ~/cs41/assign1/
myth$ /usr/class/cs41/tools/sanitycheck
myth$ /usr/class/cs41/tools/submit
```

For this assignment, we're providing both a `sanitycheck` tool and a `submit` tool.

If you're on Windows, you'll need to SSH into Stanford FarmShare (myth, corn, etc.). Hopefully, you already know how to do this, but if not, University IT has some [good solutions](https://uit.stanford.edu/service/sharedcomputing/loggingin).

### sanitycheck

The `sanitycheck` script exercises some basic functionality of your crypto module. It isn't extensive, and we'll be testing your code on more advanced test cases, but it should provide you with some confidence that everything is at least set up correctly and working properly on basic inputs.

When logged into myth (or another of the Stanford computer clusters), first navigate to your submission directory (in our case, `~/cs41/assign1/`). From there, you test your code by running

```
myth$ /usr/class/cs41/tools/sanitycheck
```

*Note: This is a new tool, and frankly, it's not perfect. There might be some bugs, so thank you in advance for being forgiving and flexible when working with our new scripts.*

### submit

When you're ready to submit, make sure that you're currently in your submission directory (that is, the output of `ls` should include `crypto.py`), and run

```
myth$ /usr/class/cs41/tools/submit
```

You should get output that looks something like:

```
Hello, sredmond
Run sanity check? (Y/N) N
Still submit?  (Y/N) Y
Uploading files to /afs/ir/class/cs41/submissions/assign1/sredmond-1
Uploading crypto.py...
Uploading design.txt...
Uploading feedback.txt...
If you have any extra files to upload (extensions, etc), you need to manually cp them to the proper directory (sorry!)
Done!
```

Note that you have the option to run sanity check before submitting.

## Notes

There are a few important things to consider:

1. Every time that you want to submit a new version of your assignment, you need to go through this whole process.
2. We'll grade the most recent assignment that you submit.
3. Make sure that you're running the `tools` scripts from inside the directory that contains `crypto.py`! Otherwise there might be some weird errors.
