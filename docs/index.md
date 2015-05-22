## Introduction and Overview

`This section is still under development.`

This guide contains instructions for installing the new OpenCV 3, on Windows from pre-built binaries, and on Ubuntu 12/14 from source code.  This page covers the installation process from start to finish, focusing finally on the Python `cv2` module itself.  Once installed, see the [**Migration & Changes**](migrating.md) page for details regarding the changes to the `cv2` module itself, and for help with migrating existing Python code from older versions of OpenCV.

To get started, OpenCV can be downloaded from [the official OpenCV website](http://opencv.org/downloads.html), or by clicking one of the two following links.  This guide is written based on OpenCV version 3.0-rc1 ([`opencv-3.0.0-rc1.exe` for Windows](http://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.0.0-rc1/opencv-3.0.0-rc1.exe/download), or [`3.0.0-rc1.zip` for Linux](https://github.com/Itseez/opencv/archive/3.0.0-rc1.zip)).  Start by downloading the appropriate version for your operating system, and extract the archive to a location of your choice.

The methods described in this document apply to both 32-bit and 64-bit operating systems/Python interpreters.  This guide is also applicable to other versions of Ubuntu (and Xubuntu/Lubuntu/Kubuntu), as well Debian and other Debian-like Linux distros.  Although OpenCV 3.0 now supports Python 3, pre-built binaries are not included with the Windows release yet - binaries for both 32-bit and 64-bit version of Python 2.7, however, is included and requires no extra configuration.  On Linux, the Python 3 module will be built if you have a Python 3 interpreter and the development header files installed before starting to compile OpenCV.

## Installing on Windows (pre-built binaries)

Support for Python 3, or adding other non-standard features, requires compiling from source.  To compile from source on Windows, see the official OpenCV documentation.

## Installing on Linux (compiling from source)

    sudo apt-get install [packages]

If you run into build issues, ensure that you have all the required dependencies and header files on your system.  If these issues persist, see the [**Linux Build Issues**](#linux-build-issues) section below for some possible workarounds.  When installing OpenCV 3.0-rc1 on Xubuntu 12.04, I found that I had to modify one of the OpenCV header files to add some additional codec `#define` lines.


## Verifying Install and Python Code Migration

You can check what version of the `cv2` module Python is using by running the following in a `python` shell:

    import cv2
    print cv2.__version__

Assuming the correct version string is printed, everything should be installed correctly at this point.  Note, however, that there are some major changes to the `cv2` module hierarchy itself, and Python programs written with OpenCV 2.4.x in mind may not work properly.  See the next section, [**Migration & Changes**](migrating.md)

## Linux Build Issues

