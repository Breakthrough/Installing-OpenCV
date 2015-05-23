
# OpenCV 3.0 Install & Python Migration Guide

----------------------------------------------------------

#### [**Click here to view the install/migration guide itself.**](https://Breakthrough.github.io/Installing-OpenCV)

----------------------------------------------------------

This repo contains the source material for the OpenCV 3.0 Installation & Python Migration Guide, which is located at [`https://Breakthrough.github.io/Installing-OpenCV`](https://Breakthrough.github.io/Installing-OpenCV).  The latest version of this guide can be [downloaded here](https://github.com/Breakthrough/Installing-OpenCV/archive/gh-pages.zip) for offline viewing, or by cloning this repo and building the documentation using [`mkdocs`](http://www.mkdocs.org/) (via `mkdocs build`, or alternatively, `mkdocs serve`).

The guide contains instructions for installing the latest stable release of OpenCV (including the Python `cv2` module), using pre-built binaries on Windows (for both 32-bit and 64-bit environments), and compiling from source on Linux (tested on Ubuntu 12.04/14.04, also applicable to Debian and other distros).  In addition, changes to the OpenCV Python interface (the `cv2` module) are also discussed, to help migrate Python code from OpenCV 2.4.x to 3.0+.

Note that this guide was written based on **OpenCV 3.0-rc1** (which can be found [on the official website](http://opencv.org/downloads.html)) and using Python 2.7.x, running on 64-bit versions of Windows 7 SP1 (with both 32-bit and 64-bit Python environments) and Xubuntu 12.04 / 14.04.  Note that although OpenCV now includes support for Python 3, a binary release is not yet included, and must be compiled from source.  This guide is also applicable for other versions of Ubuntu (and Xubuntu/Lubuntu/Kubuntu), as well Debian and other Debian-like Linux distros.

----------------------------------------------------------

Except where explicitly stated otherwise, the contents of this repository are hereby released into the public domain.

Copyright (C) 2015 Brandon Castellano.  All rights reserved.
