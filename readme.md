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
    - Break demo: have all connect to cassander with their key
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
    - Building a server machine in your lab: basic concepts
    - Saving and backing data up (version control?)
    - Walkthrough of all instruments in the lab
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
Fortunately, somebody has done the legwork for me: [python4photonics Getting Started](https://python4photonics.org/gettingstarted/).

Make sure you:
* Are able to launch a jupyter notebook with python 3
* Are familiar with numpy arrays and some scipy example functions
* Have plotted at least one thing with matplotlib (just to test if the rendering is alright)

### Extra
* Bring a MATLAB code you have done in the past (we are going to python that in the workshop)

## Version control and Git

### Start with an introductory video. Options:
- [Git and GitHub for Poets, part 1.1](https://www.youtube.com/watch?v=BCQHnlnPusY)

### 15-minute exercise
[Self-learn tutorial](https://try.github.io/)

### Now an exercise of collaboration:
Let us all edit someone's [PhD thesis](http://www.jeffdwoskin.com/dissertation/#template) from EE department, typeset in Latex.
* Go to https://github.com/lightwave-lab

### References
[Community git book](https://book.git-scm.com/docs)

## A small intro to UNIX and bash

## More general references
[Python 4 Photonics](https://python4photonics.gitlab.io)
