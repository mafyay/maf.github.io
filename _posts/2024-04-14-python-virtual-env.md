---
title: Quick Guide - Python Virtual Environment
date: 2024-04-14 09:52:00 +0100
categories: [python, code]
tags: [python, terminal, code, venv]     # TAG names should always be lowercase
---

Creating a Python virtual environment for each Python project you work on is a best practice that truly pays off. By isolating each project, you can easily switch between them, regardless of library versions. Besides, when clearly specifying which libraries and versions are being used, you facilitate development for others who may want to contribute, and for you (who, for example, wants to carry on developing in another computer, or has left a project accumulating dust for a while and wants to pick it up again).

Despite the usefulness of this practice, actually doing it for the first time is a bit daunting. What is a Python virtual environment? How do I even create one? These very important questions can make any person run away from the task. But it's truly not that bad! Allow me to explain.

## Concept

Python virtual environments are a sort of a container. They are a way to isolate the development of a project, keeping everything nice and tidy.

Each virtual environment contains:
- A specific version of Python;
- The set of libraries used, as well as their respective versions.

The libraries you install in a virtual environment are contained in that virtual environment. They won't interfere with other projects.

## 1. Create a virtual environment

To create a virtual environment, first choose the place where you want it to exist in. Let's call this place `venvPath`, for the purposes of the tutorial.

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

This will create a folder called `.venv` in our `blog-project` folder.

## 2. Use (activate) the virtual environment

To activate the virtual environemnt, run one of the following commands, depending on your shell (correctly replacing `venvPath`, of course):

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

However, these steps are not meant to be followed sequentially. You can, for example, do 3.1, then immediately write all the libraries you know you'll use, then do 3.3. Or do 3.1, then 3.2 as many times as necesssary.
They are just organized like this for logic and explanation purposes.

### 3.1 Keep track of dependencies
Before installing any libraries, we must create the following files in the root of our project folder:

1. **(Mandatory)** *requirements.txt* - This is the file where we will keep a list of the libraries used, and their versions;
2. (Optional) *requirements-dev.txt* - This is a list of libraries that are important only in development. The name doesn't have to be exactly like this.

Each file will have one library per line, as follows:
```
library1==v.v.v
library2==v.v.v
...
```
Where `v.v.v` is the version, in this format (but with numbers instead of v's, of course).

### 3.2 Install libraries

Now, we can install packages as we always do, by first running the following command:
```shell
pip install library1
```

After doing so, we must add the necessary lines to the files we created in the previous step.

### 3.3 Use requirements.txt to install dependencies

To use *requirements.txt* to install all our dependencies at once, we can simply run the following command (whilst having the virtual environment activated):
```shell
pip install -r requirements.txt
```

The same idea applies to *requirements-dev.txt*.

## Final thoughts

I hope this quick guide has brought some clarity on the core idea of a Python virtual environment, as well as how to quickly get one up and running.

## Sources
- [Python venv - Documentation](https://docs.python.org/3.12/library/venv.html)