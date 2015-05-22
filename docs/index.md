## Introduction and Overview

`This section is still under development.`

 The guide contains instructions for installing the latest stable release of OpenCV (including the Python cv2 module), using pre-built binaries on Windows (for both 32-bit and 64-bit environments), and compiling from source on Linux (tested on Ubuntu 12.04/14.04, also applicable to Debian and other distros). In addition, changes to the OpenCV Python interface (the cv2 module) are also discussed, to help migrate Python code from OpenCV 2.4.x to 3.0+.

This guide was written based on OpenCV 3.0-rc1 (which can be found on the official website) and using Python 2.7.x, running on 64-bit versions of Windows 7 SP1 (with both 32-bit and 64-bit Python environments) and Xubuntu 12.04 / 14.04. Note that although OpenCV now includes support for Python 3, a binary release is not yet included, and must be compiled from source. This guide is also applicable for other versions of Ubuntu (and Xubuntu/Lubuntu/Kubuntu), as well Debian and other Debian-like Linux distros.

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

