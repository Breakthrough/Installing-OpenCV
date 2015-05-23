## Introduction and Overview

`This section is still under development.`

This guide contains instructions for installing the new OpenCV 3, on Windows from pre-built binaries, and on Ubuntu 12/14 from source code.  This page covers the installation process from start to finish, including the OpenCV Python interface (provided by the `cv2` module).  Once installed, see the [**Migration & Changes**](migrating.md) page for details regarding the changes to the `cv2` module itself, and for help with migrating existing Python code from older versions of OpenCV.

To get started, OpenCV can be downloaded from [the official OpenCV website](http://opencv.org/downloads.html), or by clicking one of the two following links.  This guide is written based on OpenCV version 3.0-rc1 ([`opencv-3.0.0-rc1.exe` for Windows](http://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.0.0-rc1/opencv-3.0.0-rc1.exe/download), or [`opencv-3.0.0-rc1.zip` for Linux](https://github.com/Itseez/opencv/archive/3.0.0-rc1.zip)).  Start by downloading the appropriate version for your operating system, and extract the archive to a location of your choice.

The methods described in this document apply to both 32-bit and 64-bit operating systems/Python interpreters.  Although OpenCV 3.0 now supports Python 3, pre-built binaries are not included with the Windows release yet - binaries for both 32-bit and 64-bit version of Python 2.7, however, is included and requires no extra configuration.  On Linux, the Python 3 module will be built if you have a Python 3 interpreter and the development header files installed before starting to compile OpenCV.

## Installing on Windows (pre-built binaries)

Support for Python 3, or adding other non-standard features, requires compiling from source.  To compile from source on Windows, see the official OpenCV documentation.

Using pre-built binaries is the quickest way to get a Python OpenCV environment up and running on Windows.  The pre-built [Python packages provided by Christoph Gohlke](http://www.lfd.uci.edu/~gohlke/pythonlibs/) are very useful in this regard, and referenced below in the module dependencies.


#### Downloading OpenCV and Python

To begin, ensure you have downloaded ([`opencv-3.0.0-rc1.exe` for Windows](http://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.0.0-rc1/opencv-3.0.0-rc1.exe/download) from the OpenCV website, and extracted it to a directory of your choice.

Before continuing, ensure that you have a working Python 2.7 installation, which can be downloaded from [the Python website](https://www.python.org/).  This guide was tested using Python 2.7.9 ([x86 installer](https://www.python.org/ftp/python/2.7.9/python-2.7.9.msi) / [x64 installer](https://www.python.org/ftp/python/2.7.9/python-2.7.9.amd64.msi)).  When installing, it is recommended that you allow the installer to add Python to your `PATH` environment variable, so you can run `python` and `pip` from any command prompt.

Note that in the following section, you should download the Python modules for the correct version of the interpreter you have (either 32-bit or 64-bit).


#### Installing Module Dependencies

To use the Python OpenCV `cv2` module, we need to ensure the `NumPy` and `SciPy` stack is available.  To do this, first ensure that you have a working `python` environment, and have `pip` installed (if not, use the links above, and ensure the Python folder is in your `PATH` variable).  Installing the following Python modules requires `pip`.

Start by downloading the pre-built [NumPy Module](http://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy) and [SciPy Module](http://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy), installing them using the `pip install [module].whl`.  Note that you should download the version corresponding to your Python version (2.7 in this case) and word length.  For example, on 32-bit systems/interpreters:

    pip install numpy-1.9.2+mkl-cp27-none-win32.whl
    pip install scipy-0.15.1-cp27-none-win32.whl

And for 64-bit systems/interpreters:

    pip install numpy-1.9.2+mkl-cp27-none-win_amd64.whl
    pip install scipy-0.15.1-cp27-none-win_amd64.whl

After installing, you should be able to `import numpy` and `import scipy` from a Python interpreter to verify that the modules were installed correctly.


#### Installing Python-OpenCV Module


## Installing on Linux (compiling from source)

Although this guide is written for Ubuntu 12.04/14.04 and other variants (e.g. Xubuntu/Lubuntu/Kubuntu), the process should largely be the same on other versions, as well as similar Debian-like Linux distributions.  Pay attention to the output of each command to ensure everything worked correctly, and if there are any issues during the build process, see the bottom of this document for possible mitigations

#### Downloading OpenCV

To begin, ensure you have downloaded [`opencv-3.0.0-rc1.zip` for Linux](https://github.com/Itseez/opencv/archive/3.0.0-rc1.zip) from the OpenCV website, and extracted it to a directory of your choice (e.g. `~/opencv-src`).  Create a `build` folder inside the folder where the archive was extracted (the directory containing the `CMakeLists.txt` file), and open a terminal session there.  For example:

    # Assuming the files were extracted to ~/opencv-src/...
    cd ~/opencv-src
    mkdir build
    cd build

Execute all of following commands from the `build` sub-folder itself, so the compiled files will be placed there.


#### Installing Build Dependencies

Let's ensure we have all of the required dependencies to compile OpenCV, including the build tools themselves.  Execute the following commands to acquire the minimum required packages:


Note that for additional OpenCV modules/features (e.g. GPU/CUDA support, or Python 3 module), you will need to download the respective development/SDK packages for those libraries as well.  The dependencies listed above only cover building OpenCV itself and the Python 2.7 `cv2` module.


#### Compiling and Installing OpenCV

a


      mkdir build
      cd build

a


    sudo apt-get install [packages]

If you run into build issues, ensure that you have all the required dependencies and header files on your system.  If these issues persist, see the [**Linux Build Issues**](#linux-build-issues) section below for some possible workarounds.  When installing OpenCV 3.0-rc1 on Xubuntu 12.04, I found that I had to modify one of the OpenCV header files to add some additional codec `#define` lines.


## Verifying Install and Python Code Migration

You can check what version of the `cv2` module Python is using by running the following in a `python` shell:

    import cv2
    print cv2.__version__

Assuming the correct version string is printed, everything should be installed correctly at this point.  Note, however, that there are some major changes to the `cv2` module hierarchy itself, and Python programs written with OpenCV 2.4.x in mind may not work properly.  See the next section, [**Migration & Changes**](migrating.md)

## Linux Build Issues

