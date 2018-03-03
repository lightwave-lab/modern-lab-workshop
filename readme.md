# Modern lab collaboration and automation workshop

We are going to discuss some techniques to make our lives a little easier and our data a lot more professional, documented, and reproducible. 

## Workshop Agenda

* 8:20AM - Welcome and settling in. Macbooks charging. Internet connection ok etc.
* 8:30AM - Introduction, outline
* 8:45AM - An engineer's guide to modern lab control (part 1)
    - What is version control / git (15 minutes)
    - 15-minute exercise
    - Cloning and collaborating from github (15 minutes)
    - A small intro to UNIX and bash
    - Digital security + private key authentication + 2FA
    - Break demo: have all connect to cassander/github with their key
* 10:00AM - break (installation of homebrew + virtualenv + python3 + jupyter)
* 10:15AM - Messing around with python
    - Features of a programming language (coming from MATLAB) - python as example
    - Scientific computing: numpy, scipy and matplotlib
    - Getting comfortable reading source code and documentation
        + The __init__ file
        + __doc__ docstrings
        + navigating modules with sublime or github.
    - Awesome python data processing and plotting demo
* 11:15PM - Q&A session about individual projects (part one)
* 12:00PM - Lunch break
* 1:30PM - An engineer's guide to modern lab control (part 2)
    - Why centralized control
    - GPIB, USB and Serial protocols
    - Ethernet, TCP, IP, Socket
    - Instruments, hosts, servers, clients
    - Saving and backing data up (version control?)
* 2:15PM - Break
* 2:30PM - Demo sessions (Eric, HT, Tait et al.)
    - HT: SIMPEL: quick overview of cython integration
    - Eric: Live experiment control
    - Lamia: Parsing data and regularization algorithm
    - Tait: Virtual experiment
* 3:30PM - Walkthrough of lightlab package
* 4:15PM - Princeton Resources
* 4:30PM - Q&A session about individual projects (part two)
* 5:30PM - fin

## Preparation from home

### Some reading
* [Using Python to Automate your Experiments (pg. 9)](https://www.photonicssociety.org/images/files/publications/Newsletter/2018-FebWeb.pdf)

### Make an account in github.com
* add a profile picture so I can recognize you.
* Find an opensource project you like and star it or fork it

### Make sure you have installed:
* [Sublime](www.sublimetext.com)
* [Latex](https://www.latex-project.org/get/)

### Install python somehow
* Windows is painful, I recommend [Anaconda](https://conda.io/docs/_downloads/conda-cheatsheet.pdf) to deal with it.
* macos
    - I like this tutorial from [Marina Mele](http://www.marinamele.com/2014/07/install-python3-on-mac-os-x-and-use-virtualenv-and-virtualenvwrapper.html) to install python3 from brew and work with virtualenvwrapper.
    - caveat: there will be a lot of installation bugs if you had tried to install python in a different way in the past, e.g. download binary from python directly, anaconda for mac, macports etc. I recommend using brew and pip from python3 for everything.
* linux
    - I am going to assume you know what you are doing if you are using linux. Make sure you have virtualenv and python 3.6 installed

### Get started
Fortunately, somebody has done the legwork for me: [python4photonics Getting Started](https://python4photonics.gitlab.io/gettingstarted/).

Make sure you:
* Are able to launch a jupyter notebook with python 3
* Are familiar with numpy arrays and some scipy example functions
* Have plotted at least one thing with matplotlib (just to test if the rendering is alright)

### Extra
* Bring a MATLAB code you have done in the past (we are going to python that in the workshop)

# Workshop notes

## Version control and Git

### Start with an introductory video. Options:
- [Git and GitHub for Poets, part 1.1](https://www.youtube.com/watch?v=BCQHnlnPusY)

### 15-minute exercise
[Self-learn tutorial](https://try.github.io/)

### Now an exercise of collaboration:
Let us all edit someone's [PhD thesis](http://www.jeffdwoskin.com/dissertation/#template) from EE department, typeset in Latex.
* Go to https://github.com/lightwave-lab/modern-lab-workshop
* Clone the repository
* Open the project with sublime (install shortcut with subl)
* Small demo with LatexTools installed (compilation and opening)
    - Compile with Cmd-B
    - Check Pdf (Cmd-L v) if you have Skim installed
    - Clean files with (Cmb-L Backspace)
* Manual compilation command:
    - `latexmk -cd -f -pdflatex -interaction=nonstopmode -synctex=1 /path/to/thesis.tex`
    - `-cd` - Change to directory of source file when processing it
    - `-f` - force continued processing past errors
    - use the `./clean.sh` script to delete auxiliary files.
* Make a `.gitignore` file inside `01-git-exercise-latex` to ignore latex temporary files as well as the generated `thesis.pdf`. Check if it worked with `git status`.

Now make edits to the files and follow the instructions to add changes to stage, commiting and pushing.

TODO: Insert commands used for that

## Intro to UNIX and bash

TODO: Insert here the commands used while going through the slides.

## Digital security and private key authentication

Let's make a private key. The default one is stored in `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`.

The main command is `ssh-keygen`. We will follow the instructions in [Connecting to GitHub with SSH](https://help.github.com/articles/connecting-to-github-with-ssh/)

## Installation of python environemnt

### Instructions for macOS

Mostly taken from [Marina Mele](http://www.marinamele.com/2014/07/install-python3-on-mac-os-x-and-use-virtualenv-and-virtualenvwrapper.html)

```bash
#First, have the xcode Command Line Tools. These are the basic compilers you need to get started. Install with 
xcode-select --install

# Then, install homebrew, which is a repository of pre-built opensource packages (if there is no build for your OS version, it will default to compilation from source code. Neat!)

ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# I think brew installation already writes the following line to your .bash_profile, but in case it doesn't, do it yourself.

# First, verify it's there. Restart your terminal, and run
echo $PATH
# /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/TeX/texbin:/opt/X11/bin

# If it isn't, it is safe to add it to ~/.bash_profile
# open editor 
nano ~/.bash_profile
# And then copy this line in the bottom
export PATH=/usr/local/bin:$PATH
# Exit nano while saving with Ctrl-X, Yes, Enter. Restart your terminal

# Before continuing, it might be a good idea to inspect whether brew sees some problem in your system that would cause it to malfunction
brew doctor

# Then, with Brew installed, install python3
brew install python3

# Verify version with:
python3 --version
# Python 3.6.4
which python3
# /usr/local/bin/python3
which pip3
# /usr/local/bin/pip3

# If you don't have the results above please stop and fix the bash_profile until you do.

# We can skip pyvenv's instructions...

# Installing virtualenvwrapper
pip3 install virtualenv virtualenvwrapper

# Configure virtualenvwrapper
# First, create the folder your virtualenvs will live:
mkdir ~/Envs

# Then, add the following line to your ~/.bashrc
export WORKON_HOME=~/Envs
export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3
source /usr/local/bin/virtualenvwrapper.sh

# Restart the terminal, or execute
source ~/.bashrc

# Create your first virtual environment (note that autocomplete works)
mkvirtualenv standard
# Using base prefix '/usr/local/Cellar/python3/3.6.4_2/Frameworks/Python.framework/Versions/3.6'
# ...

# This will automatically activate the virtual environment. it should show (standard) at your bash caret
# Useful commands:
deactivate  # exits the virtualenvironment
rmvirtualenv envname  # removes virtualenv envname
workon envname  # activates virtualenv name. You can switch very easily between virtual environments.

# From inside your virtual environment, we will install basic python packages
pip install jupyter numpy scipy matplotlib

```

If the above executed with no errors, then you're good to go. For users of other OS, make sure you are inside a virtual environment, with pip and these packages installed: jupyter numpy scipy matplotlib

## Messing around with python

Go into `02-messing-around-with-python` and start a notebook server:

```bash
workon standard
jupyter notebook
```

Cheating: https://lectures.quantecon.org/py/index.html

## VISA control

From your mac: https://stackoverflow.com/questions/5541096/ni-visa-pyvisa-on-mac-os-x-snow-leopard

## References
* [Community git book](https://book.git-scm.com/docs)
* [An introduction to Linux Permissions](https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-permissions)
* [More information on Unix permissions](https://en.wikipedia.org/wiki/Unix_security)
* [Python 4 Photonics](https://python4photonics.gitlab.io)
