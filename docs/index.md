
## Introduction and Overview

This document contains instructions for installing and migrating to the latest release of OpenCV (version 3) and the Python bindings.  In addition to some API changes, there are also changes to the Python interface (e.g. removal of `cv2.cv`) that may require changes in existing code to work with the new version of the `cv2` module.  After installation, see the next page, [**Migration & Changes**](migrating.md), for details regarding the changes to the module and for help migrating existing Python code to the new version.


------------------------------------------------------


This page covers installing OpenCV 3 on Windows (using pre-built binaries) and Linux (compiled from source), including the Python interface (the `cv2` module).  OpenCV can be downloaded from [the official OpenCV website](http://opencv.org/downloads.html).  Note that this guide is written based on OpenCV version **3.0-rc1**.  After installation, it is recommended that you can check the version of OpenCV that Python is using:

```python
import cv2
print cv2.__version__

# Should print 3.0.0-rc1 or newer.
```

Note that although OpenCV 3.0 is the latest release, by convention, the module is still named `cv2`.


------------------------------------------------------


## Installing on Windows (pre-built binaries)

Using pre-built binaries is the quickest way to get a Python OpenCV environment up and running on Windows.  Currently, only the Python 2 version of the `cv2` module is built and included in the latest Windows release.  Support for Python 3 (as well as adding other non-standard features/modules), requires compiling from source - see the official OpenCV documentation for details.


#### Downloading OpenCV and Python

To begin, [download OpenCV](http://opencv.org/downloads.html) for Windows ([version 3.0 RC1, `opencv-3.0.0-rc1.exe`](http://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.0.0-rc1/opencv-3.0.0-rc1.exe/download)), and extract it to a directory of your choice.  The Windows build includes both a 32-bit and 64-bit module for Python 2.7.

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

Lastly, we need to copy the OpenCV module into the local Python packages.  In the files extracted from `opencv-3.0.0-rc1.exe`, go to the folder `opencv\build\python\2.7\`, and open either the `x86\` (for 32-bit) or `x64\` (for 64-bit) folder.  In each, there will be a `cv2.pyd` file.

Copy `cv2.pyd` directly into the `Lib\site-packages\` directory of your Python installation.  For most users, this will be found at:

```bash
C:\Python27\Lib\site-packages 
```

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

To compile OpenCV, we must ensure that the required dependencies are available, including the build tools themselves.  We can get the required ones using `apt` on Ubuntu, but first, ensure the package list is up-to-date by running `apt-get update`.  Next, execute the following commands to get the required packages (see below for a one-line list of all):

```bash
sudo apt-get install cmake build-essential pkg-config

sudo apt-get install libgtk2.0-dev libtbb-dev

sudo apt-get install python-dev python-numpy python-scipy

sudo apt-get install libjasper-dev  libjpeg-dev libpng-dev libtiff-dev 

sudo apt-get install libavcodec-dev libavutil-dev libavformat-dev libswscale-dev

sudo apt-get install libdc1394-22-dev libv4l-dev
```

Note that for additional OpenCV modules/features (e.g. GPU/CUDA support, or Python 3 module), you will need to download the respective development/SDK packages for those libraries as well.  The dependencies listed above only cover building OpenCV itself and the Python 2.7 `cv2` module.


#### Compiling and Installing OpenCV

Now that we have the required build dependencies, run `cmake` (again, in the `build/` directory we created) to generate the Makefile to build OpenCV:

```bash
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
```

If there are any errors, ensure that you downloaded all the required packages - the output should help track down what is missing.  To ensure the Python module will be built, you should see `python2` in the list of configured modules after running `cmake`:
    
    [...]

    --     Linker flags (Release):
    --     Linker flags (Debug):
    --     Precompiled headers:      YES
    --
    --   OpenCV modules:
    --     To be built:              hal core flann imgproc ml [...] python2

    [...]

If you do not see the `python2` module listed, in the "To be built" list, check that you have the proper Python development packages installed, remove all files from the `build/` folder, and try running the `cmake` command again.

Now, we can build OpenCV (and the Python module) using `make`, and install it to our system:

```bash
make
sudo make install
```

**Ensure that the build was successful after calling `make`, and check the output before installing.** If you run into build issues/errors, again ensure that you have all the required dependencies and header files on your system.  If there are actual build issues with OpenCV itself, see the [**Linux Build Issues**](#linux-build-issues) section below for some possible workarounds.

When installing OpenCV 3.0-rc1 on Ubuntu 12.04, I ran into build errors regarding some missing codec `#define` entries.  As mentioned, the steps to do this are [detailed below](#linux-build-issues) should you run into the same problem.  Conversely, on Ubuntu 14.04, the build completed successfully without any modifications.

If the build was successful, but you can't `import cv2` from a Python shell after running `make install`, you can install the module manually by copying the `cv2.so` file we just built in the `build/lib/` folder to `/usr/local/lib/python2.7/dist-packages/`.  From the `build/` folder, this can be done by:

```bash
sudo cp lib/cv2.so /usr/local/lib/python2.7/dist-packages/
```

After this step, the `cv2` module is installed, and can now be imported by your Python environment. Continue on to the [Verifying Installation](#verifying-installation) section to ensure everything was installed correctly, and more importantly, that the correct version of OpenCV is being used by Python.  You can also check out the next page, [Migration & Changes](migrating.md), for details about changes to the `cv2` module, and what changes need to be made to existing code to run with the updated module.


------------------------------------------------------


## Verifying Installation

As mentioned previously, you can verify that the `cv2` module was installed correctly by executing the following in a Python shell:

```python
import cv2
print cv2.__version__
```

If the correct version string is printed (`3.0.0-rc1` or newer if you used a more recent version), everything is installed correctly at this point!

Note that there are some major changes to the `cv2` module hierarchy itself, and Python programs written with OpenCV 2.4.x in mind may not work properly anymore.  See the next section, [**Migration & Changes**](migrating.md) for details about the changes, and how to modify programs to deal with the changes.


------------------------------------------------------


## Linux Build Issues

On some systems you may run into issues when compiling OpenCV itself, depending on what packages are available.  If the proper header files are available, but build issues still arise, try to see if there are any workarounds below for the problem.


#### Undefined `AV_CODEC_ID_...` in `ffmpeg_codecs.hpp`

If you run into an issue where build errors are caused by certain codecs not being defined, you can download a more recent version of `ffmpeg_codecs.hpp` [from here](https://github.com/Itseez/opencv/blob/master/modules/videoio/src/ffmpeg_codecs.hpp), and replace it in the source code you downloaded/extracted in the `modules/videoio/src/` folder.

 Alternatively, you can declare them manually by editing the `ffmpeg_codecs.hpp` file itself by adding the missing codec entry for `H263I`, and renaming `WNV` to `WNV1`.  You can see what changes have to be made by viewing [this commit from the OpenCV GitHub project](https://github.com/Itseez/opencv/commit/f052b0bc4d2619daafe5c56d91fc4a6cb00b8b7c).

 Once the file is updated, you can call `make` again from the `build/` folder, and OpenCV should finish compiling without error now.
