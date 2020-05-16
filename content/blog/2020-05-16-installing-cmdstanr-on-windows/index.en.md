---
title: Installing CmdStanR on Windows
author: Max
date: '2020-05-16'
slug: cmdstanr-windows
categories:
  - R
  - Stan
tags:
  - stan
  - cmdstanr
  - windows
  - ubuntu
toc: yes
images: ~
---

In this post I will share a few tips and tricks about installing CmdStanR on Windows. I write these down to not forget them myself, but maybe someone will find them useful as well. _This page might be subject to change. It is not an official installation guide._

## Why CmdStanR

Over the past few years I have done a lot of statistical modeling in [Stan](https://mc-stan.org/). I remember [this great blog post by Wayne Folta](https://thinkinator.com/2016/01/12/r-users-will-now-inevitably-become-bayesians/), which finally pushed me to switch from ``lme4`` and the likes to ``rstanarm`` and ``brms``. However, soon I started writing all my models in "pure" Stan using the ``rstan`` package. I just loved that Stan made me think more deeply about my models and the nearly endless flexibility it gave me to tackle my specifc research questions. 

While ``rstan`` is a great package with a lot of extremely useful features, such as ``expose_stan_functions``, my love for it has grown a little colder recently. It always nagged me that it lagged behind in what "real" Stan, i.e. [CmdStan](https://mc-stan.org/users/interfaces/cmdstan.html), could do. As far as I understand, this has to do with the fact that ``rstan`` has to go through an extremly tedious process to be on CRAN. But knowing that Stan had great features, such as ``map_rect`` and more recently ``reduce_sum``, and not being able to use them, because ``rstan`` was several versions behind, felt somewhat disappointing. Also, while running fine most of the time, [sometimes ``rstan`` can mess with your R session](https://discourse.mc-stan.org/t/most-stable-stan-interface-s/13870), which can make for a fairly frustrating experience.

Luckily, the Stan devs started working on "lightweight wrappers around CmdStan" for [R](https://mc-stan.org/cmdstanr/) and [Python](https://cmdstanpy.readthedocs.io/en/latest/). Since I mainly use R, I gave the ``cmdstanr`` package a try. Using R 3.6 (and RTools 3.5) on Windows 10 everything worked great. I could just go through the _[Getting Started with CmdStanR](https://mc-stan.org/cmdstanr/articles/cmdstanr.html)_ vignette and it ran right out the box. My models compiled faster and I could use all the cool new features.

Unfortunately, I recently ran into a few problems installing CmdStanR. All of them could eventually be solved with the help of the awesome Stan devs at [discourse.mc-stan.org](https://discourse.mc-stan.org/). The following post is a collection of notes, mainly to myself, on how to install CmdStanR on Windows. I hope that some of you might find these helpful and more of you are enclined to try CmdStanR.

**Note that the ``cmdstanr`` package is work in progress. The devs are working hard on making the installation process as smooth and well documented as possible.**

## CmdStanR on Windows 10

### R 4.0 and RTools 4.0

R 4.0 comes with RTools 4.0 and some of the things changed compared to the former versions of RTools. You still need to make sure that RTools is in your ``PATH``. For RTools 4.0 you need to add

```
C:\RTools\RTools40\usr\bin
C:\RTools\RTools40\mingw64\bin
```

to you ``PATH`` (see [these instructions](https://helpdeskgeek.com/windows-10/add-windows-path-environment-variable/), if you are not sure how to add something to your ``PATH``). You might have to change these lines to point to the correct location of your RTools 4.0 installation. Another thing to look out for is any [Anaconda](https://www.anaconda.com/) installation you might have on your system. Usually, it is sufficient to put the path to RTools _before_ the path to Anaconda in your ``PATH``.

When I upgraded to R 4.0 with RTools 4.0 and tried to install CmdStanR, I got an error message telling me that ``mingw32-make`` could not be found. You actually have to install ``mingw32-make`` manually via _RTools Bash_. To open RTools Bash, which comes with RTools 4.0, just hit **Windows Key**, type ``rtools bash`` and hit **Enter**. A new console window will pop up. Now, just type

```bash
pacman -Sy mingw-w64-x86_64-make
```

and you should be ready to go. To see if everything is set up correctly you can run the follwing three lines in the terminal (**Windows Key**, type ``cmd`` and hit **Enter**):

```
g++ --version
```

{{< image src="win10-rt40-g++.png" alt="win10-rt40-g++" position="center" style="border-radius: 3px;" >}}

```
bash --version
```

{{< image src="win10-rt40-bash.png" alt="win10-rt40-bash" position="center" style="border-radius: 3px;" >}}

```
mingw32-make --version
```

{{< image src="win10-rt40-make.png" alt="win10-rt40-make" position="center" style="border-radius: 3px;" >}}

If all of them return output containing a version number and are not pointing to the Anaconda distribution (if installed), you should be good to go.

You can now open RStudio and run 

```r
# you might need to install devtools
devtools::install_github("stan-dev/cmdstanr")
library(cmdstanr)
install_cmdstan()
```

and I suggest you work through the _[Getting started with CmdStanR](https://mc-stan.org/cmdstanr/articles/cmdstanr.html)_ vignette.

### R 3.6 and RTools 3.5

The installation of CmdStanR on Windows 10 with R 3.6 and RTools 3.5 ran really smoothly. My guess is that some people might run into trouble when they did not include RTools in their ``PATH``. If you don't know how to add something to ``PATH``, you can check out [these instructions](https://helpdeskgeek.com/windows-10/add-windows-path-environment-variable/). In case you have RTools 3.5 installed, you need to add 

```
C:\RTools\RTools35\bin
C:\RTools\RTools35\mingw_64\bin
```

to your ``PATH`` (check whether these point to the correct directories and adjust accordingly). Another thing to look out for is any [Anaconda](https://www.anaconda.com/) installation you might have on your system. Usually, it is sufficient to put the path to RTools _before_ the path to Anaconda in your ``PATH``.

To see if everything is set up correctly you can run the follwing four lines one by one in the terminal (**Windows Key**, type ``cmd`` and hit **Enter**):

```
g++ --version
bash --version
mingw32-make --version
```

If all of them return output containing a version number and are not pointing to the Anaconda distribution (if installed), you should be good to go.

You can now open RStudio and run 

```r
# you might need to install devtools
devtools::install_github("stan-dev/cmdstanr")
library(cmdstanr)
install_cmdstan()
```

and I suggest you work through the _[Getting started with CmdStanR](https://mc-stan.org/cmdstanr/articles/cmdstanr.html)_ vignette.


## CmdStanR on Windows 7

The ``PATH`` to RTools has to be set just as under Windows 10, so check out the corresponding description above depending on which version you have of RTools (3.5 or 4.0).

The major difference on Windows 7 is that it does not come with ``curl``, which is needed for installing CmdStan via ``install_cmdstan()`` (see [this thread](https://discourse.mc-stan.org/t/win7-cant-find-stanc-exe-when-using-cmdstanr-install-cmdstan-solved/13846/9) for reference).

**UPDATE:** AS OF CmdStanR 2.23, CURL IS NO LONGER REQUIRED TO INSTALL CmdStan TROUGH ``install_cmdstan()``. THE FOLLWING APPLIES ONLY IF YOU WANT TO INSTALL AN OLDER VERSION OF CmdStan.

You can either 

- Install CmdStan manually (check the thread in the link above, or _[Getting started with CmdStan](https://github.com/stan-dev/cmdstan/wiki/Getting-Started-with-CmdStan)_) and use ``set_cmdstan_path(PATH_TO_CMDSTAN)`` after installing ``cmdstanr``,
- if you have Git for Windows, add ``C:\Program Files\Git\mingw64\bin\`` to your ``PATH`` (again, check [this link](https://helpdeskgeek.com/windows-10/add-windows-path-environment-variable/) if you are not sure how to do this),
- if you have RTools 4.0 installed, you can try the _RTools Bash_ (**Windows Key**, type ``rtools bash`` and hit **Enter**) and run ``pacman -S curl`` _(I haven't verified this yet)_.

To verify if everything is set-up correctly check the follwing line by line in a new terminal (**Windows Key**, ``cmd``, **Enter**):

```
g++ --version
bash --version
mingw32-make --version
curl --version
```

Now, you can switch to RStudio and run (if you did not install CmdStan manually):

```r
# you might need to install devtools
devtools::install_github("stan-dev/cmdstanr")
library(cmdstanr)
install_cmdstan()
```

Again, I suggest you work through the _[Getting started with CmdStanR](https://mc-stan.org/cmdstanr/articles/cmdstanr.html)_ vignette from here on.

## CmdStanR via WSL

With Windows 10 came the possiblity to run a full fledged Linux distribution within Windows via the _Windows Subsytem for Linux_ (WSL). The installation process is fairly easy, but before we get into that, why would you want to run CmdStanR through WSL? One reason is that installing and running CmdStan (through CmdStanR) is generally easier and more robust compared to Windows once you have set everything up in Linux. Another advantage of running CmdStan on Linux is that it is [likely faster than on Windows](https://discourse.mc-stan.org/t/large-cmdstan-performance-differences-windows-vs-linux/14415).

As far as I know it is not possible to run programs with graphical user interfaces directly in WSL. There are some workarounds, however. I simply installed RStudio Server, which works nicely. But first, let's start with WSL.

### Installing WSL

I found the installation of WSL to be surprisingly easy. This is party due to the fact that the process _is_ relatively easy, but also due to the great [Installation Guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10), which I want to refer to here. I basically just followed these instructions and installed WSL1. I chose Ubuntu 18.04 LTS and would recommend you do the same (unless you know what you are doing, but in this case you probably should not have to read this anyways). Note that you do not need a Microsoft account when downloading Ubuntu from the store. You can simply skip when being asked to sign in.

### Installing R and RStudio Server

When you have successfully installed Ubuntu 18.04 LTS you can start it by pressing the **Windows Key**, typing ``ubuntu`` and hitting **Enter**. You'll be asked to set a username and password. 

To install R 4.0 you can follow the [instructions on the CRAN website](https://cran.r-project.org/bin/linux/ubuntu/#installation), but I go through these step by step as I found them a bit confusing.

I won't pretend I know a lot (or even a little) about Linux. Apparently you need to add keys to securely install software from new sources. So let's begin with adding the key for our CRAN download. Make sure to [enable copy-and-paste functionality in your WSL console](https://devblogs.microsoft.com/commandline/copy-and-paste-arrives-for-linuxwsl-consoles/) before starting. This will hopefully save you a lot of typing and squinting. 

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
```

Next we need to add the CRAN repository for R 4.0 to the ``sources.list`` file. First, we'll back-up the file by making a copy with an ``.bak`` extension. (Note, that everything below assumes that you are in your user ``~`` directory. If you are not, type ``cd ~`` to go back there.)

```bash
sudo cp ../../etc/apt/sources.list ../../etc/apt/sources.list.bak
```

Now, we add the line ``deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran40/`` at the end of the file.

```bash
echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran40/" | sudo tee -a ../../etc/apt/sources.list
```

You can verify that the line is added to the end of the file by typing:

```bash
cat ../../etc/apt/sources.list
```

The next few lines will install R 4.0. This might take a little while.

```bash
sudo apt-get update
sudo apt-get install r-base
sudo apt-get install r-base-dev
```

Now you can run R in the terminal: Just type ``R`` to start and ``q(save = "no")`` to quit without saving.

{{< image src="ubuntu-r40-example.PNG" alt="ubuntu-r40-example" position="center" style="border-radius: 3px;" >}}

Before we go on and install RStudio Server, we install a few libraries that we will need later on. Just run these three lines one by one.

```bash
sudo apt-get install libssl-dev
sudo apt-get install libcurl4-openssl-dev
sudo apt-get install libxml2-dev
```

Now we are ready to install RStudio Server. You can check out their [Download RStudio Server for Debian & Ubuntu](https://rstudio.com/products/rstudio/download-server/debian-ubuntu/) page (scroll down to Ubuntu 18), but it's basically the same as written here.

Again, before installing let's add the key (remember you can use copy-paste; see above).

```bash
gpg --keyserver keys.gnupg.net --recv-keys 3F32EE77E331692F
```

The next few lines will install RStudio Server for Ubuntu 18.

```bash
sudo apt-get install gdebi-core
wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.2.5042-amd64.deb
sudo gdebi rstudio-server-1.2.5042-amd64.deb
```

You are now ready to go. RStudio Server should already be running. In Windows, open your browser and type `localhost:8787`. Sign in using your Linux credentials (username and password, which you specified earlier) and you should be good to go. 

If RStudio Server is _not_ running, you will get an *Unable to connect* or *This site can’t be reached* error. Open the the Ubuntu shell and type 

```bash
sudo rstudio-server start
```

to start the server. You can find a few more useful commands [here](https://support.rstudio.com/hc/en-us/articles/200532327-Managing-the-Server).

### Installing CmdStanR

Once you have opened RStudio Server you can use R just like you are used to. Before installing the ``cmdstanr`` package from GitHub, you need to install ``devtools``. Let's also install all of it's dependencies. Be warned that this might take a while. Furthermore, it is useful to specify ``INSTALL_opts = c("--no-lock")``, because otherwise the ``xml2`` package will probably not install correctly (see [here](https://askubuntu.com/questions/1163130/permission-denied-while-installing-r-package)).

```r
install.packages(
  "devtools", 
  dependencies = TRUE, 
  INSTALL_opts = c("--no-lock")
  )
```

After installing ``devtools``, installing ``cmdstanr`` should be easy:

```r
devtools::install_github("stan-dev/cmdstanr")
```

And with CmdStanR it is easy to install CmdStan.

```r
library(cmdstanr)
install_cmdstan()
```

From here on, you can go through the aforementioned _[Getting started with CmdStanR](https://mc-stan.org/cmdstanr/articles/cmdstanr.html)_ vignette to see whether CmdStanR is working correctly. 

The only question remaining is how to access your Windows files and how to get the results out of RStudio Server back to Windows. 

You can actually access all your Windows files in the `mnt/` directory. For example, all your Windows files in your `C:\` drive can be found in `mnt/c/`. By default your user has no access to these directories. I strongly advise you to only give permission to the folders which contain your R and Stan projects. On my laptop this is ``D:\data\`` in Windows, which is ``mnt/d/data/`` in Ubuntu. You want to be able to read and write files in this and all of its subfolders. Assuming you are at `~` (type ``cd ~``, if you are not) you can simply run 

```bash
sudo chmod -R +rw ../../mnt/d/data/
```

where you have replaced the last bit to correspond to the folder which you want to give permission for. The ``-R`` states that this command is applied recursively to all subfolders. The ``+rw`` states that you grant _read_ and _write_ permission. Note, that we did _not_ give permission to execute programs (that would have been ``+rwx``), because executing programs here might cause problems. This also means that you can not run Stan models which are stored here via your Ubuntu installation of CmdStanR. (Remember that _"running a Stan model"_ is actually _"running a Stan program"_.) You'd need to copy them to somewhere else in your home directory in Ubuntu. You can, however, just save the CSV containing the draws of you model fit, plots, tables, etc. to your Windows drive.

## Wrapping up

That's it! I hope this was useful for some people. I will likely come back to this and update parts of this post. So please feel free to comment and leave feedback. Please remember that this is not an official installation guide. If you have questions you can leave them here, or search the [Stan Forums](https://discourse.mc-stan.org/) for answers.
