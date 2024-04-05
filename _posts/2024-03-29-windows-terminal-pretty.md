---
title: Windows Powershell - The Makeover
date: 2024-03-29 19:38:59 +0000
categories: [code, windows]
tags: [windows, terminal, code, powershell]     # TAG names should always be lowercase
---

If, like me, you're a macOS user who has recently decided to give Windows a chance, or if you're just starting to use the PowerShell a bit more, and you've simply thought to yourself, "Huh, does it really have to look like this?", then you've come to the right place!

In this post I will explain how to use [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts) and [Oh My Posh](https://ohmyposh.dev/) to achieve a (much) better-looking Windows PowerShell.

This post is based heavily on [TroubleChute's tutorial](https://www.youtube.com/watch?v=-G6GbXGo4wo) [[1](#sources)], so I **really** recommend watching it first, as I think it will be enough. I'm only writing this post because, while following it, I stumbled upon a few problems. Therefore, I intend to compile, in a single source, both the steps to beautifying the PowerShell, but also some problems that may arise while doing it, as well as their respective solutions. I also intend to be as brief and clear as possible.

As is the main objective of this blog, this post is intended to serve as documentation for myself. However, I'm publishing it online in the hopes that it may be useful to anyone who finds it.

That's it. Now, let's get to it!

## The How-To

### 1. Prerequisites
#### Have Windows Powershell installed
If you do not have the Windows Powershell installed, go to the Microsoft Store and install "Windows Terminal".

#### Have Winget installed
Run the command `winget` in the PowerShell. If you get an error like **winget: The term 'winget' is not recognized as the name of a cmdlet, function, script file or operable program. (...)**, then go to the Microsoft Store, search for "winget" and install "App Installer".

### 2. Edit theme
Open the PowerShell. Now we'll begin!

Choose a (prettier) theme and edit it to your liking in *Settings* > *Cholor schemes*. I went with "One Half Dark", edited with a slightly lighter background color.

### 3. Install Nerd Fonts
This is necessary! It will be important in the next step.

Go to [Nerd Fonts - Releases](https://github.com/ryanoasis/nerd-fonts/releases), click on the most recent one, scroll down to *Assets* and choose one to your liking.

When the download finishes, unzip the file, select all the *.otf* files, right-click and select *Install*.

Finally, go to the PowerShell, select *Settings* > *(Profile) Defaults* > *(Additional settings) Appearance* > *Font face*, and select any one of the newly-installed fonts, like, for example, *FiraCode NFM*.

I installed *FiraCode* (Nerd Fonts version [v3.1.1](https://github.com/ryanoasis/nerd-fonts/releases/tag/v3.1.1)), just like in the previously [tutorial](https://www.youtube.com/watch?v=-G6GbXGo4wo).

### 4. Install Oh My Posh

Let's follow the Oh My Posh [documentation](https://ohmyposh.dev/docs/installation/windows).

Open a PowerShell prompt and run the following command:

```shell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

Now close and re-open the PowerShell, then run the following command. This will set up your PowerShell with a default Oh My Posh theme.

```shell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json" | Invoke-Expression
```
To see a list of available themes, either go to [Oh My Posh - Themes](https://ohmyposh.dev/docs/themes) or run the following command:
```shell
Get-PoshThemes
```

After that, choose a theme that you like. For example, I've chosen the [amro](https://ohmyposh.dev/docs/themes#amro) theme. We can try the chosen theme out by running the following command:
```shell
oh-my-posh init pwsh --config 'C:\Users\USERNAME\AppData\Local\Programs\oh-my-posh\themes\amro.omp.json' | Invoke-Expression
```
You can substitute the *USERNAME* in the path with yours, or you can just copy and paste the command that Oh My Posh suggested after you ran the previous command. To try any other theme, substitute *amro* in the path with the correct name for your theme, which is usually the exact name of the theme itself.

To make that theme stick (that is, to make it show up everytime you open the PowerShell), run the following command. If you are using any shell that's not *powershell*, please follow the [instructions](https://ohmyposh.dev/docs/installation/prompt) suited to your shell instead.
```shell
notepad $PROFILE
```

If this gives an error, run the following command first, and then the previous one again.
```shell
New-Item -Path $PROFILE -Type File -Force
```

This will open up an empty file in Notepad. In there you will write the expression with the Oh My Posh theme you've chosen. So, for example, since I chose the *amro* theme, I wrote:
```shell
oh-my-posh init pwsh --config 'C:\Users\USERNAME\AppData\Local\Programs\oh-my-posh\themes\amro.omp.json' | Invoke-Expression
```

Now save and close the previous file. After doing so, run the following command. This will ensure the changes take effect.
```shell
. $PROFILE
```

And that's it! Yay!


## Problems and Fixes

### Problem 1: cannot be loaded because running scripts is disabled on this system

If at some point you run into this error: **cannot be loaded because running scripts is disabled on this system**, then follow the next steps to fix it:

1. Open the PowerShell by right-clicking on it and selecting “Run as Administrator”

2. Run the following command:
```shell 
Set-ExecutionPolicy RemoteSigned
```

This should fix it and allow you to continue your customization.

To understand the root cause of, and to read a bit more about this problem, please visit [Salaudeen Rajack's tutorial](https://www.sharepointdiary.com/2014/03/fix-for-powershell-script-cannot-be-loaded-because-running-scripts-is-disabled-on-this-system.html) [[2](#sources)]. It is a very clear and useful read!

### Problem 2: Get-PSReadLineKeyHandler : A parameter cannot be found that matches parameter name 'Key'.

If you find this error: **Get-PSReadLineKeyHandler : A parameter cannot be found that matches parameter name 'Key'**, then run the following command:

```shell
Install-Module PsReadLine -Force
```

I also met this error while following this process, and jfrmilner's answer to Bipul Hf's question in [this Stack Overflow question](https://stackoverflow.com/questions/75499007/get-psreadlinekeyhandler-a-parameter-cannot-be-found-that-matches-parameter-na) [[3](#sources)] is what fixed it for me.

## Final Notes
![Screenshot of the Windows PowerShell with the result of the customizations done throughout this post.](/assets/post_imgs/my-pretty-powershell.png)
_The final product - better, right?_

I hope this post was helpful to anyone that may have read it.

If anything seems wrong or is not working, please tell me!

## Sources
1. [Make Windows Terminal Look Better Oh My Posh Guide - TroubleChute @ YouTube](https://www.youtube.com/watch?v=-G6GbXGo4wo)
2. [Fix for PowerShell Script cannot be loaded because running scripts is disabled on this system error - Salaudeen Rajack @ SharePoint Diary](https://www.sharepointdiary.com/2014/03/fix-for-powershell-script-cannot-be-loaded-because-running-scripts-is-disabled-on-this-system.html)
3. [Get-PSReadLineKeyHandler : A parameter cannot be found that matches parameter name 'Key'. What is this in Oh My Posh? - Bipul Hf @ Stack Overflow](https://stackoverflow.com/q/75499007)
4. [ASMR Set Up PowerShell with Oh-My-Posh on Windows 11 + Neovim Setup + Terminal Icons - No Talking - Bek Brace @ YouTube](https://youtu.be/fviSilPKIhs?si=nRjtZBtG72URHWC3)