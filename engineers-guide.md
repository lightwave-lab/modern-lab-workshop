# An engineer’s guide to modern lab control

## Introduction

Over the years, software engineering has evolved into a very prominent field that penetrates all industrial sectors. Its core principles and philosophy was to make life easier for consumers to achieve their goals. That was when Apple and Microsoft were created. Then, as the field evolved, it has become important to make software engineering as inclusive as possible to new “developers”, and to make collaboration as seamless as possible. This is the age of the apps. Now, software programming is becoming considered as fundamental as math and science, and are starting to enter school curricula.

Meanwhile, in academic circles and other engineering industries have lagged in software sophistication. Here, I propose a few techniques that we can borrow from software engineering to make our collaborative work in the lab more productive. My inspiration draws from the fact that in software engineering teams, the source code describes the entirety of a product. And if it is well documented, a new member of the team can learn and understand how it works in high or low level without the need for person-to-person training. In other words, all knowledge is documented in source code, instead of a mind hive. This is not the case in research groups. When a PhD student leaves, all his or her know-how suddenly exits the lab.

## The concepts

### Software programming

The first tool that is instrumental to this method is software programming. Computers were created with the intention to automate or facilitate menial tasks. The tendency is to delegate more and more of our labor to the machine, so we can move on to the bigger picture.

In our lab, a scientific experiment depends on controlling many instruments at the same time. The more complex the experiment, as they ten to be with integrated circuits, the more instruments are needed and the more complicated the calibration procedures and execution algorithms are. Most of these instruments are designed to have an electronic interface compatible with computers. These can be chiefly USB, which stands for Universal Serial Bus, or GPIB, for General Purpose Interface Bus, or Ethernet. Through these ports, computers can launch commands and probe results at the speed that the interface supports. As a result, one can control instrumentation of an experiment via the computer, i.e. via software. This is called a cyber-physical system. But this is not all. Software can also be used to perform any kind of algorithm. Which means that in a cyber-physical host, an experiment can be _defined_ entirely by a computer program.

Computers programs can be written in a programming language, such as Python, MATLAB, C, Fortran, Java etc. There are many, but they all have the same purpose: to translate english words into machine code. Over a century of math, engineering, logic, and language science has passed since [Ada Lovelace](https://en.wikipedia.org/wiki/Ada_Lovelace) wrote the first algorithm intended for a machine. Python is a very modern language, still in active development, that became ubiquitous in the software engineering world due to its flexibility. It is considered a high-level language, meaning that its representation is very close to plain English, while its machine inner-workings are very hidden insides. Normally, these programming languages result in programs that are slower than the ones written in a more low-level language. Python’s popularity stems from the fact that it can directly interface with a lot of these other faster languages, and it is fast enough for most people with modern computers. It also offers myriad open-source libraries that offer everything from web apps to numerical simulation to deep learning. So Python nowadays is the favorite first language of scientists, engineers, developers, students etc.

### Version control

It is possible to use a particular programming language to write routines and small scripts that can have inputs, crunch some numbers, and produce outputs. However, actual programming languages were created to support Turing complete applications, which support an infinite complexity of internal states and behaviors. When source code became too complicated, i.e. around the time of the [Apollo missions](https://github.com/chrislgarry/Apollo-11), computer scientists invented object-oriented programming, which made possible the modularization of source codes. This meant that programmers could change a piece of the code that interacted with the entire application without necessarily having to fully understand the entire source code. As a result, programmers needed a central location to store the code so they could edit it at the same time. This was called version control. Version control has become standard in all industries that deal with software. It is so efficient that it allows thousands of programmers to collaborate on an opensource project, each one submitting small changes, without risking introducing new bugs.

There are many technical ways to achieve version control, and many different software written to accommodate these techniques. The most popular are Git, Subversion, Mercurial and Microsoft’s Team Foundation Server. Like it or not, today, Git dominates the version control software arena, and is rendering the others rather obsolete. So let’s talk about version control as designed by Git’s developers.

![Distributed Version Control System, such as Git.](https://git-scm.com/book/en/v2/images/distributed.png)

#### Version control with Git

![](https://ih0.redbubble.net/image.390578060.2383/flat,800x800,075,f.u1.jpg)

The most basic concept of version control is revision tracking. Every revision to the source code is recorded by a “commit”. The commit records the changes made by the user respective to the previous revision. You can think of it as a linear graph, where the nodes represent the different revisions of the entire source code and the arrows the history connecting them. This is useful because the history of any project is automatically recorded and documented. Teams also use this feature to track how active their developers are. 

![Storing data as snapshots of the project over time.](https://git-scm.com/book/en/v2/images/snapshots.png)

Commits are created and stored in what is called a repository, which is a data structure that keeps track of all commits made in history. In Git, this repository is stored in your computer, so that you can interact with it offline. The process typically works as follows. You work on the documents and code normally with your favorite editor, changing them on disk. When you have finished a desired set of changes, you create a commit and document what you have included in that particular commit, so that future you or collaborators have a sense of what changes were made before looking into the code. When a commit is triggered, the software automatically detects the changes that were made to every file, including whether it was deleted, renamed, or whether its metadata was changed. It then creates a manifest of all these changes, compresses it, and generate what is then called a “commit”. After that, the commit is automatically stored in your “local repository”, which is hidden inside a folder named “.git”. 

```
git commit -m “message”
```

There are two concepts which, at this point, confuses most people unfamiliar with version control: staging and remote vs. local. But they are not complicated at all. The concept of staging can be understood by the following example. Say that there is a project/repository with two main parts: a numerical simulation part, and an experimental data processing part. Their code is contained in different files. You have made changes to both of these files because you are working on them at the same time, but you have finished implementing a desired change in the simulation file, but the one on experimental data is still in progress. Therefore, if you want to commit the changes you have made on the simulations while ignoring the rest, a staging step is necessary prior to commit. You add the simulation file to what is called a stage, leaving the experimental processing out of the stage. This allows you to commit only what is on the stage. 

```
# Edit simulation file
git add simulation.py
git commit -m “finished simulation”
```

![Working tree, staging area, and Git directory.](https://git-scm.com/book/en/v2/images/areas.png)

Another interesting property of Git is its ability to separate remote and local copies of the repository. In order to make the source code available to others, it needs to be uploaded somewhere remote. That is the raison d’être of a remote repository. There are web services that can host remote repositories, most famously GitHub, where virtually all the opensource projects are stored nowadays. The local copy of the repository is an exact and entire copy of the remote one, that is why one must “clone” it to the local computer. Clone, in this case, means download the current version plus all other versions in history. Therefore, after a commit is created in the local repository, it must be “pushed” to the remote copy so others can  see it and “pull” to their local copy.

```
# Edit simulation file
git add simulation.py
git commit -m “finished simulation”
git push
```

![How git push works.](https://wac-cdn.atlassian.com/dam/jcr:f148974e-7d4d-4c0e-bd31-8ac5467d1e6a/04.svg?cdnVersion=ie)

The other main property of Git is that it can automatically “merge” a number of edits together in one step. Its algorithm is very powerful, works flawlessly when it can, and falls back to human intervention in case of “conflicts”. When two collaborators create local commits, their history tree forks into two parallel versions that need to be conciliated. If one pushes first, the other’s push will fail and abort, because its local repository does not agree with the most recent state of the remote repository. So the proper procedure is to sync the local with the remote by “pulling” changes from remote:

```
# Edit simulation file
git add simulation.py
git commit -m “finished simulation”
git pull  # this is where the merge happens
git push
```

![C6 is the merge between C5 and C4.](https://git-scm.com/book/en/v2/images/basic-merging-2.png)

The merge algorithm works in the following way. It attempts to add all modifications from both revisions to a stage. First, if the modified files are different, then both files are simply added to the stage. If the same file is modified, then Git will start a “diff” operation. It will go through line by line on each revision of the file until it detects a discrepancy. The revisions considered are the baseline (the revision agreed upon prior to the commit), the remote, and the local. Each discrepancy is judged as addition, deletion or simply edits. If Git detects a discrepancy both in the remote and the local commits, then a conflict is triggered, and the user must resolve it themselves by choosing to maintain changes from one revision or the other, or altering the line altogether. After the merge operation is finished, all files are added to the stage and a _new_ commit is created. This commit is special because it has two “parents”, so the history graph will look like three branches which merged together. Note that this process is designed such that no changes are lost during merge. It is an automatic way of doing a very tedious task that humans used to do in the past.

[Here](https://git-scm.com/docs/gittutorial) is a tutorial on Git.

### Servers, hosts and clients

In order to make this all work, we need _servers_, _hosts_, and _clients_. A computer server can refer to the software or the device used in the “[client—server](https://en.wikipedia.org/wiki/Client–server_model)” model. So you can have many _software_ servers running on different _server_ machines. As you can see, it can get complicated really fast. So unless otherwise specified, let us understand the word server as powerful computers that are expected to be turned on and connected to the network at all times.

A _host_ is any computer (or device) connected to the network. So all servers are hosts, but not all hosts are servers. If one wants to be able to control a certain instrument via the network, this instrument should either be a host itself or be connected to one via some interface bus. There are so many ways to do this that it would be counterproductive to introduce them all. But it is important to understand why these hosts cannot be servers. Simply, when you connect a new instrument to the host, sometimes one must install new software, update software drivers, or even reboot the machine. Stuff that cannot be allowed on a server that serves multiple clients at the same time.

Finally, a _client_ is a workstation that depends on resources offered by the server. It can be our personal computers.

In most research laboratories that require some sort of automation, researchers typically use one single computer to directly connect to the instruments that execute the experiment. A scientist can do this, download the data to her personal computer, go home, and crunch the numbers. This has been a good enough practice for simple experiments where there was a single person dealing with the instrumentation and the data analysis. However, when multiple persons need to have access to the most recent data, or even access to the experiment, it makes more sense to have a client—server—host implementation. In software engineering, the source code of some large projects such as Facebook grew to hundreds of gigabytes, with compilation times up to days. For them, having the source code stored and compiled on a supercomputer server is crucial.


### Instrument drivers

Instrument drivers are pieces of code responsible to command and control instruments. For example, a Keithley 2400 source meter can be controlled via GPIB protocol. National Instruments offers a set of low-level drivers ([NI-VISA](http://www.ni.com/tutorial/3702/en/)) that can be installed in Linux or Windows hosts, which allows us to establish connection, send and receive GPIB (or, more modernly, VISA) commands easily. These are files that have to be installed directly into the operational system. Then, we can install an opensource package called [PyVISA](http://pyvisa.readthedocs.io/en/stable/), written in Python, which interfaces with the low-level NI-VISA drivers. The lightlab package contains an object built onto PyVISA, representing the Keithley 2400 instrument. This object contains functions that can translate commands such as turn on, turn off, ramp up current or voltage, read resistance, voltage or current values; into VISA commands that can be sent through the NI-VISA drivers. This object can be accessed directly from the Jupyter notebook.


## Appendix
### Bash
### Digital security
#### Private keys
#### Two-factor authentication
