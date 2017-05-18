QSsh [![Build Status](https://travis-ci.org/wang-boyu/QSsh.svg?branch=master)](https://travis-ci.org/wang-boyu/QSsh)
---

QSsh provides SSH and SFTP support for Qt applications. The aim of this project 
is to provide a easy way to use these protocols in any Qt application.
This project is based on Qt Creator's libQtcSsh.so. All the credits to
Qt Creator's team!

### Prerequisites

- Qt 5.3 or later 
- On Windows: MinGW 4.7 or later, Visual Studio 2010 or later
- On Mac: XCode 6.4 or later, Qt5 installation prefix should be added into `CMAKE_PREFIX_PATH` if building with CMake

Compiling QSsh:

```bash
$ mkdir $BUILD_DIRECTORY
$ cd $BUILD_DIRECTORY
$ qmake $SOURCE_DIRECTORY/qssh.pro
$ make (or mingw32-make or nmake depending on your platform)
```

or you can open "qssh.pro" with "Qt Creator".

### Examples

- Directory examples/ssh/ 
