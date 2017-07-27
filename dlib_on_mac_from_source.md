## Step 1: Get dlib prerequiisites

The dlib library only has four primary prerequisites:

* [Boost](http://www.boost.org/): Boost is a collection of peer-reviewed (i.e., very high quality) C++ libraries that help programmers not get caught up in reinventing the wheel. Boost provides implementations for linear algebra, multithreading, basic image processing, and unit testing, just to name a few.
* [Boost.Python](http://www.boost.org/doc/libs/1_57_0/libs/python/doc/index.html): As the name of this library suggests, Boost.Python provides interoperability between the C++ and Python programming language.
* [CMake](https://cmake.org/): CMake is an open-source, cross-platform set of tools used to build, test, and package software. You might already be familiar with CMake if you have used it to compile OpenCV on your system.
* [X11](https://en.wikipedia.org/wiki/X_Window_System)/[XQuartx](https://www.xquartz.org/): Short for “X Window System”, X11 provides a basic framework for GUI development, common on Unix-like operating systems. The macOS/OSX version of X11 is called XQuartz.

## Step 2: [Install Homebrew - the whole thing](https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/)

Or simply these two steps

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    brew update
        



## Step 3: Get python

    brew install python
    brew install python3
    brew install cmake
    brew install boost
    brew install boost-python --with-python3
      
## Step 4: Check your installation
    brew list | grep 'boost'
    boost
    boost-python
        
## Step 5: Get required packages for dlib

    pip install numpy
    pip install scipy
    pip install scikit-image

## Step 6: Time to install dlib

    pip install dlib
    
    
## Problems you are likely to run into

### dlib make fails for various reasons

* Error 1 : Build fails
        make[2]: *** No rule to make target `/Users/username/anaconda/lib/libpython3.6.dylib', needed by `dlib.so'. <br>
Solution: `$ ln -s libpython3.6m.dylib libpython3.6.dylib`
