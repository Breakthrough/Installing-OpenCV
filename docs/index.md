## Introduction and Overview

This document contains instructions for installing and migrating to the latest release of OpenCV (version 3) and the Python bindings.  In addition to some API changes, there are also changes to the Python interface (e.g. removal of `cv2.cv`) that may require changes in existing code to work with the new version of the `cv2` module.  After installation, see the next page, [**Migration & Changes**](migrating.md), for details regarding the changes to the module and for help migrating existing Python code to the new version.

------------------------------------------------------

This page covers installing OpenCV 3 on Windows (using pre-built binaries) and Linux (compiled from source), including the Python interface (the `cv2` module).  OpenCV can be downloaded from [the official OpenCV website](http://opencv.org/downloads.html).  Note that this guide is written based on OpenCV version **3.0-rc1**.  After installation, it is recommended that you can check the version of OpenCV that Python is using:

    import cv2
    print cv2.__version__

    # Should print 3.0.0-rc1 or newer.

Note that although OpenCV 3.0 is the latest release, by convention, the module is still named `cv2`.  


------------------------------------------------------

## Installing on Windows (pre-built binaries)

Using pre-built binaries is the quickest way to get a Python OpenCV environment up and running on Windows.  Currently, only the Python 2 version of the `cv2` module is built and included in the latest Windows release.  Support for Python 3 (as well as adding other non-standard features/modules), requires compiling from source - see the official OpenCV documentation for details.


#### Downloading OpenCV and Python

To begin, [download OpenCV](http://opencv.org/downloads.html) for Windows ([version 3.0 RC1, `opencv-3.0.0-rc1.exe`](http://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.0.0-rc1/opencv-3.0.0-rc1.exe/download)), and extract it to a directory of your choice (e.g. `~/opencv-src`).  The Windows build includes both a 32-bit and 64-bit module for Python 2.7.

Before continuing, ensure that you have a working Python 2.7 installation, which can be downloaded from [the Python website](https://www.python.org/).  This guide was tested using Python 2.7.9 ([x86 installer](https://www.python.org/ftp/python/2.7.9/python-2.7.9.msi) / [x64 installer](https://www.python.org/ftp/python/2.7.9/python-2.7.9.amd64.msi)).  When installing, it is recommended that you allow the installer to add Python to your `PATH` environment variable, so you can run `python` and `pip` from a command prompt.

#### Installing Module Dependencies


The Python OpenCV `cv2` module requires both the `NumPy` and `SciPy` stack.  To get this, first ensure that you have a working `python` environment, and have `pip` installed (if not, use the links above, and ensure the Python folder is in your `PATH` variable).

Christoph Gohlke currently provides some (unofficial) [pre-built Python packages for Windows](http://www.lfd.uci.edu/~gohlke/pythonlibs/), including NumPy and SciPy.  Download the latest stable versions of [NumPy](http://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy) and [SciPy](http://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy), and install them by calling `pip install [module].whl` from a command prompt.  Note that you should download the version corresponding to your Python environment (2.7 in this case) and word length.  For example, on 32-bit systems/interpreters:

    pip install numpy-1.9.2+mkl-cp27-none-win32.whl
    pip install scipy-0.15.1-cp27-none-win32.whl

And for 64-bit systems/interpreters:

    pip install numpy-1.9.2+mkl-cp27-none-win_amd64.whl
    pip install scipy-0.15.1-cp27-none-win_amd64.whl

After installing, you should be able to run `import numpy` and `import scipy` from a Python interpreter to verify that the modules were installed correctly.  You can check what versions of NumPy and SciPy are installed from `numpy.__version__` and `scipy.__version__`, respectively.


#### Installing Python-OpenCV Module

Lastly, we need to copy the OpenCV module into the local Python packages.  In the files extracted from `opencv-3.0.0-rc1.exe`, go to the folder `opencv/build/python/2.7/`, and open either the `x86/` (for 32-bit) or `x64/` (for 64-bit) folder.  In each, there will be a `cv2.pyd` file.

Copy `cv2.pyd` directly into the `Lib/site-packages/` directory of your Python installation.  For most users, this will be found at:

    C:/Python27/Lib/site-packages 

And we're done!  Continue on to the [Verifying Installation](#verifying-installation) section to ensure everything was installed correctly, and the new version of OpenCV is being used.  Also be sure to check out the next page, [Migration & Changes](migrating.md), for details about the changes to the module and updating existing code.


------------------------------------------------------

        

## Installing on Linux (compiling from source)

Although this guide is written for Ubuntu 12.04/14.04 and other variants (e.g. Xubuntu/Lubuntu/Kubuntu), the process should largely be the same on other versions, as well as similar Debian-like Linux distributions.  Pay attention to the output of each command to ensure everything worked correctly, and if there are any issues during the build process, see the bottom of this document for possible mitigations

#### Downloading OpenCV

To begin, [download OpenCV](http://opencv.org/downloads.html) for Linux ([version 3.0 RC1, `opencv-3.0.0-rc1.zip`](https://github.com/Itseez/opencv/archive/3.0.0-rc1.zip)), and extract it to a directory of your choice (e.g. `~/opencv-src`).  Create a `build` folder inside the folder where the archive was extracted (the directory containing the `CMakeLists.txt` file), and open a terminal session there.  For example:

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


------------------------------------------------------

## Verifying Installation

As mentioned previously, you can verify that the `cv2` module was installed correctly by executing the following in a Python shell:

    import cv2
    print cv2.__version__

Assuming the correct version string is printed, everything should be installed correctly at this point.

Note that there are some major changes to the `cv2` module hierarchy itself, and Python programs written with OpenCV 2.4.x in mind may not work properly anymore.  See the next section, [**Migration & Changes**](migrating.md) for details about the changes, and how to modify programs to deal with the changes.



------------------------------------------------------

## Linux Build Issues

