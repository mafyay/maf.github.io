---
title: Quick Guide - Python Virtual Environment
date: 2024-04-14 09:52:00 +0100
categories: [programming, python]
tags: [programming, python, terminal, code, venv]     # TAG names should always be lowercase
---

Creating a Python virtual environment for each Python project we work on is a best practice that actually pays off. Why? Well,
- Isolating each project we work on means we can easily switch between them, regardless of installed libraries;
- By clearly specifying which libraries and versions we're using, we facilitate development for _(1)_ others who want to contribute, and for _(2)_ us (when, for example, want to continue development in another machine, or when we have left a project accumulating dust for a while and want to pick it up again).

Despite this practice being so useful, actually doing it for the first time is a bit daunting. What is a Python virtual environment? How do I create one? These and other questions can make any person put away the task for an indefinite amount of time. But it's truly not that bad! Allow me to explain.

## Concept

A Python virtual environment is a sort of a container. It's a way to isolate the development of a project, keeping everything tidy. Each virtual environment contains:
- A specific version of Python;
- The set of libraries used, as well as their respective versions.

The libraries you install in a virtual environment are contained in that virtual environment. They won't interfere with other projects.

## 1. Create a virtual environment

To create a virtual environment, first choose the place (_aka_ the directory) where you want it to exist in. Let's call this place `venvPath`, for the purposes of the tutorial.

Then, simply run:
```shell
 python -m venv venvPath
```
If we only provide a name, the environment will be created in the current directory with that given name. This is the usual approach. A popular virtual environment name is `.venv`.

### Example
For example, we just created a folder called `blog-project` for a project we're working on, and navigated to it in the terminal.
Now, we run:
```shell
python -m venv .venv
```

This will create a folder called `.venv` inside our `blog-project` folder.

## 2. Use (_aka_ activate) the virtual environment

To activate the virtual environemnt, run one of the following commands, depending on your shell (correctly replacing `venvPath` for the name of your virtual environment, of course):

| Platform |    Shell   | Command to activate virtual environment |
|:--------:|:----------:|:---------------------------------------:|
|   POSIX  | bash/zsh   | source venvPath/bin/activate            |
|          | fish       | source venvPath/bin/activate.fish       |
|          | csh/tcsh   | source venvPath/bin/activate.csh        |
|          | PowerShell | venvPath/bin/Activate.ps1               |
|  Windows | cmd.exe    | venvPath\Scripts\activate.bat           |
|          | PowerShell | venvPath\Scripts\Activate.ps1           |

(Taken from the [Python documentation](https://docs.python.org/3.12/library/venv.html))

## 3. Install libraries

It is *very important* that you don't skip straight to section 3.2, and **read 3.1 first**!

However, these steps don't necessarily have to be executed sequentially. You can, for example, do 3.1, then immediately write all the libraries you know you'll use (3.2), then do 3.3. Or do 3.1, then 3.2 as many times as necesssary.
They are just organized like this for logic and explanation purposes.

### 3.1 Keep track of dependencies
Before installing any libraries, we must create the following files in the root of our project folder:

1. **(Mandatory)** *requirements.txt* - This is the file where we will keep a list of all the libraries used in the project, and their versions;
2. (Optional) *requirements-dev.txt* - This is a list of libraries that are important only in development. The name doesn't have to be exactly like this.

Each file will have one library and version per line, as follows:
```
library1==v.v.v
library2==v.v.v
...
```
Where `v.v.v` is the version, in this format (but with numbers instead of v's).

### 3.2 Install libraries

Now, we can install packages as we always do, by first running the following command:
```shell
pip install library1
```

After doing so, we must add the necessary lines to the files we created in the previous step. This means that everytime we add a library to our project, we must specify it in the _requirements.txt_ file.

### 3.3 Use _requirements.txt_ to install dependencies

To use *requirements.txt* to install all our dependencies at once, we can simply run the following command (whilst having the virtual environment activated):
```shell
pip install -r requirements.txt
```

The same idea applies to *requirements-dev.txt*.

## Summary

Thus, the idea is this:
- _requirements.txt_ contains all the libraries (and their respective versions) of our project;
- Once the environemtn is activated (<a href="#2-use-aka-activate-the-virtual-environment">step 2</a>), we can can quickly install the dependencies specified in _requirements.txt_ by running the command in <a href="#33-use-requirementstxt-to-install-dependencies">step 3.3</a>.

## Final thoughts

In addition to using virtual environments, what do we do regarding our Git repository? Should the virtual environment folder be added to it? Well, the clean approach is to *not* dump your entire virtual environment folder in your Git repository, but instead adding a README file with a **Run** section, where you explain **How to create a virtual environment** and **How to install the requirements**. This way, anyone that clones the repository has only to follow those steps.

That's it. I hope this brief guide brought some clarity on the core idea of what a Python virtual environment is, as well as how to quickly get one up and running!

## Sources
- [Python venv - Documentation](https://docs.python.org/3.12/library/venv.html)