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

* Error 2: Compilation reaches to the final `[100%] Linking CXX shared library dlib.so` but chokes in the end with bindings with these errors 
```
ld: symbol(s) not found for architecture x86_64
collect2: error: ld returned 1 exit status
make[2]: *** [dlib.so] Error 1
make[1]: *** [CMakeFiles/dlib_.dir/all] Error 2
make: *** [all] Error 2
error: cmake build failed!
```
If you have both Python 2.7 and 3.6 (anaconda in my case) installed, don't do this `brew reinstall boost-python` but this `brew reinstall boost-python --with-python3 --without-python`

The first one still links stuff with Python 2.7 as you can see below
```
==> Reinstalling boost-python --with-python3
==> Using the sandbox
==> Downloading https://dl.bintray.com/boostorg/release/1.64.0/source/boost_1_64_0.tar.bz2
Already downloaded: /Users/tarrysingh/Library/Caches/Homebrew/boost-python-1.64.0.tar.bz2
==> ./bootstrap.sh --prefix=/usr/local/Cellar/boost-python/1.64.0 --libdir=/usr/local/Cellar/boost-python/1.64.0/lib --with-libraries=python --with-python=python --with-pyth
==> ./b2 --build-dir=build-python --stagedir=stage-python python=2.7 --prefix=/usr/local/Cellar/boost-python/1.64.0 --libdir=/usr/local/Cellar/boost-python/1.64.0/lib -d2 -j==> ./bootstrap.sh --prefix=/usr/local/Cellar/boost-python/1.64.0 --libdir=/usr/local/Cellar/boost-python/1.64.0/lib --with-libraries=python --with-python=python3 --with-python-root=/usr/local/Cellar/python3/3.6.2/Fr
==> ./b2 --build-dir=build-python3 --stagedir=stage-python3 python=3.6 --prefix=/usr/local/Cellar/boost-python/1.64.0 --libdir=/usr/local/Cellar/boost-python/1.64.0/lib -d2 -j8 --layout=tagged --user-config=user-conf
🍺  /usr/local/Cellar/boost-python/1.64.0: 462 files, 28MB, built in 2 minutes 46 seconds
```
while the `brew reinstall boost-python --with-python3 --without-python` avoids Python 2.7 all together
```
==> Reinstalling boost-python --without-python --with-python3
==> Using the sandbox
==> Downloading https://dl.bintray.com/boostorg/release/1.64.0/source/boost_1_64_0.tar.bz2
Already downloaded: /Users/tarrysingh/Library/Caches/Homebrew/boost-python-1.64.0.tar.bz2
==> ./bootstrap.sh --prefix=/usr/local/Cellar/boost-python/1.64.0 --libdir=/usr/local/Cellar/boost-python/1.64.0/lib --with-libraries=python --with-python=python3 --with-python-root=/usr/local/Cellar/python3/3.6.2/Fr
==> ./b2 --build-dir=build-python3 --stagedir=stage-python3 python=3.6 --prefix=/usr/local/Cellar/boost-python/1.64.0 --libdir=/usr/local/Cellar/boost-python/1.64.0/lib -d2 -j8 --layout=tagged --user-config=user-conf
🍺  /usr/local/Cellar/boost-python/1.64.0: 454 files, 15.2MB, built in 1 minute 29 seconds
```
