---
title: "The EIC Software Environment"
teaching: 10
exercises: 20
questions:
- "What is the EIC environment?"
objectives:
- "Understand what we mean with the EIC environment, or `eic-shell`."
- "Appreciate the benefits of containers as development environment."
keypoints:
- "The EIC environment `eic-shell` is a singularity/docker container with a curated selection of software components."
---
## Why a EIC standard environment?
- EIC software is modular, so not just a matter of a single `make install` command but close to 20 necessary dependencies and 10 EIC-specific packages.
- Laboratory operating systems are stable and (therefore) slow to upgrade to new versions, even though we need those version in the modern software we write:
  - gcc-11 or gcc-12 for C++17 ranges, C++20 for concepts and filtered ranges, and C++23 for zipped ranges
  - underlying dependencies like ACTS, DD4hep, podio, etc, each have many options, some of which are important to set right (or you end up with a DD4hep that doesn't do some of the things we need it to do)
- The standard environment gives all users access to exactly the same environment that is used for benchmarks, productions, and continuous integration on the github and gitlab servers.
- The standard environments are versioned and can be retrieved (or rebuilt) at a later time in case you wish to revisit an old result. Specifying the specific version of the standard environment you used for a particular plot will definitively determine what versions of e.g. geant4 and ROOT you used.
- If you encounter a bug that you can reproduce in a standard environment, it makes it much much easier for software developers to fix. Making it easier for developers to fix you bug will typically result in your bug getting fixed quicker. If developers cannot reproduce the bug, it often becomes a fishing expedition that few developers have appetite for.

## Are you required to use the EIC standard environment?
- No. You can use any environment you want. We are merely trying to make this easy for all users to get started, in particular if you are not yet familiar with compiling source code from scratch.
- Most of the people in the software groups use a mix of the standard environment and other installations (for example, we may have ROOT installed separately).
- We may ask you to reproduce issues that you observe in the standard environment before we can act on them.
- If there is a specific workflow or use case that you cannot achieve in the standard environment, let us know and we'll work with you to address that.

## How to get `eic-shell`, the EIC standard environment, and what it is?
- The EIC standard environment is accessed with the `eic-shell` command. That will start an `eic-shell` session in the standard environment.
- To install the `eic-shell` command in the directory `~/eic/` (which you may need to crate), you can run the following command:
```console
cd ~/eic
curl --location https://get.epic-eic.org | bash
```
- You can also save the file at https://get.epic-eic.org as `install.sh` and run this script by hand:
```console
cd ~/eic
wget --output-document install.sh https://get.epic-eic.org
bash install.sh
```
- The install script will search for several components that are required (see the prerequisites):
  - which operating system you are running (linux and mac are supported),
  - whether you have singularity or docker installed (see prerequisites),
  - whether you have access to the Cern VM file system at `/cvmfs` (typically available on clusters, and can be easily installed on individual linux systems, see https://cernvm.cern.ch/fs/).
- If you are on a system that requires downloading the full container (up to 10 GB), this may take a while and no progress bar is shown.
- The install script will create a new file `./eic-shell` which will start the `eic-shell` environment, i.e. the EIC standard environment.

> Note: An alternative location for downloading this script is at https://eicweb.phy.anl.gov/containers/eic_container/-/raw/master/install.sh, in case you experience difficulties accessing the custom domain.
{: .callout}

> Note: On some high performance computing servers, there are security restrictions that require the use of additional flags `curl --insecure` and `wget --no-check-certificate`.
{: .callout}

> Exercise 1:
> - Install the `eic-shell` executable in a suitable location on the system you will be using mainly for EIC work.
> - Look at the output and compare with what is on the instructor's screen. If you do not have a `/cvmfs` directory on your system, this may take a while as the environment has to be downloaded. Keep this in mind for later, as you will have to perform updates periodically.
> - Advanced users: Take a look at the installation options when you run `bash install.sh --help`. The include information on how to tweak your setup for specific use scenarios.
{: .challenge}

## How to start `eic-shell` on common systems?
You can start `eic-shell` from inside the directory where it is installed with
```console
cd ~/eic
./eic-shell
```
or you can start it from any directory with `~/eic/eic-shell` (if you used the same directory structure).
- When you have successfully started `eic-shell` you should see a `jug_xl> ` prompt, indicating that you are now **inside** the EIC standard environment.
- Pro-tip: You can also add the directory where `eic-shell` is installed to your search path, so you can start `eic-shell` from anywhere. Or you can install `eic-shell` in a directory that is already in your search path.

> Exercise:
> - Run the `eic-shell` script from the current directory. You should get the `jug_xl> ` prompt. Exit the environment again.
> - Take a look at the running options with `eic-shell --help`. If you do not have a `/cvmfs` directory on your system, you will need to run `eic-shell --upgrade` periodically to ensure that you are staying up to date.
> - Advanced users: Set up your environment to be able to run `eic-shell` from anywhere.
{: .challenge}

## What is where in the eic-shell environment?
When you start `eic-shell`, you enter into a container: a self-contained operating system that integrates with the core of the operating system on the host system. When you look at the top-level directories, you'll see that they are similar to the directories on the host system. Don't let that fool you: you are looking at content that is only inside the container.

There are a few directories that are shared between the container and the host operating system: the current directory you are working on, your home directories, etc. Essentially, the typical directories where you would store your own work (as opposed to system directories).

All programs that are installed in the container, are accessible under the `/usr/local` directory tree. This is a standard location for programs that are not installed by the operating system's package manager, which is how we install the dependencies for the EIC software stack. It also means that these programs are automatically found by the `eic-shell` without needing to modify the search path.

The jumble of files in `/usr/local` are in fact merely a view into software installed in a more organized fashion in `/opt/software`, potentially for different compilers, operating systems, etc. The full definition of all software installed in `/opt/software` is in `/opt/spack-environment/dev/spack.yaml`, the ultimate definition of the EIC standard environment.

> Exercise:
> - Using `cd` and `ls`, check that you can navigate to various directories in the container, and that you can access the directories for your own work.
> - Verify that you can run some of the software dependencies that are installed in `eic-shell`. For example, run the command `ddsim --help` to get some informaton on one way to run Geant4 simulations on DD4hep-based geometries. Use the command `which ddsim` to see where `ddsim` is located.
> - Advanced users: Based on the location of `ddsim` found in the previous step, verify that this is a symbolic link to a different location under `/opt/software`. Verify that the version in the path of that location agrees with the version specified in the `spack.yaml` file.
{: .challenge}

## Notes on starting graphical programs
Graphical programs work just as well inside the `eic-shell` environment as outside, with the exception of docker on Mac where some additional work is needed. On a Mac it is therefore often easier to open ROOT files outside the container.

{% include links.md %}
