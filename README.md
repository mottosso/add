### add

minimal, cross-platform additive environments for your shell.

![untitled](https://cloud.githubusercontent.com/assets/2152766/16431552/09bf25e6-3d79-11e6-9b31-24dc727d6a63.gif)

<br>
<br>
<br>

### Installation

**Windows**

```bash
$ git clone https://github.com/mottosso/add
$ set PATH=%cd%\add;%PATH%
```

**Linux**

```bash
$ git clone https://github.com/mottosso/add
$ export PATH=$(pwd)/add:$PATH
```

**MacOS**

```bash
$ git clone https://github.com/mottosso/add
$ export PATH=$(pwd)/add:$PATH
```

<br>
<br>
<br>

### Usage

`add` only has a single command and no flags.

```bash
$ add myenv
```

The single argument calls upon a similarly named shell script, `env-myenv.bat` for Windows and `env-myenv.sh` for any other platform.

`env-myenv.x` is a any regular shell script.

#### Example 1 - A Python environment

In this example, we'll assume a freshly installed Windows OS, with an isolated distribution of Python 2 located at `c:\python27`. Isolated, as in, calling `python` from the terminal should result in..

```bash
$ python
'python' is not recognized as an internal or external command,
operable program or batch file.
```

Start by creating the module itself.

**env-python.bat**

```bash
@echo off
set PATH=C:\Python27;C:\Python27\Scripts;%PATH%
```

Save this anywhere on your `PATH`. For example.

```bash
$ move env-python.bat c:\bin
$ set PATH=c:\bin;%PATH%
```

Now you can add Python 2 to your environment by calling `add`.

```bash
$ add python
$ python
Python 2.7.11 (v2.7.11:6d1b6a68f775, Dec  5 2015, 20:40:30) [MSC v.1500 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

#### Example 2 - Composite environments

Now let's take one step further and build a composite environment of many sub-environments, such as the development environment for one of your projects where you might use Python, as before, but also PyQt and perhaps other libraries.

Rather than typing these in all by hand, we can set one environment call all of them.

**env-myproject.bat**

```bash
@echo off
call add python
call add python-qt5
call add my-library
call add my-other-library
```

Now you have yourself a shortcut to a larger enviroment.

```bash
$ add myproject
$ python
Python 2.7.11 (v2.7.11:6d1b6a68f775, Dec  5 2015, 20:40:30) [MSC v.1500 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import PyQt5
>>> import my_library
>>>
```

<br>
<br>
<br>

### Introduction

This "utility" - if it can even be called that - is more of a mindset than a piece of software. It is based on the core principle of [modules](http://modules.sourceforge.net/), an early 21st century command-line utility to manage complex environments and [Rez](https://github.com/nerdvegas/rez) an environment.

But rather than giving you all of what it has to offer, it only offers one thing. To blindly and carelessly add one environment on top of another.

**Why?**

Where the environment is a haystack, your problem is the needle.

Keeping the haystack small and manageble is often hard, especially without simple practices and clear mental image of how to mould it.

This is what `add` is designed to solve.

<br>
<br>
<br>

### Module Files

`modules` has a concept of module files within which you specify a complete environment for a given application or library. This module can then be loaded, alongside other modules that you have loaded, resulting in a larger environment which is the sum of all currently loaded modules.

You can use these modules to build complex combinations of environment on-the-fly, or pre-define combinations up-front and build entire presets with a single command.

In `add`, these are plain executable shell scripts; `.bat` for Windows, `.sh` for Linux. In fact, any executable shell script will do, it doesn't matter.

**env-python.bat**

```bat
@echo off
set PATH=C:\Python27;C:\Python27\Scripts;%PATH%
```

Here is a module which adds Python 2.7 to the active environment, enabling a user to launch an interactive Python session.

```bash
$ add python
$ python
```