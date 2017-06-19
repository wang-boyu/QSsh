QSsh [![GitHub version](https://badge.fury.io/gh/wang-boyu%2FQSsh.svg)](https://badge.fury.io/gh/wang-boyu%2FQSsh) [![Build Status](https://travis-ci.org/wang-boyu/QSsh.svg?branch=master)](https://travis-ci.org/wang-boyu/QSsh) [![Build status](https://ci.appveyor.com/api/projects/status/xkjjowbsc8tc3otd/branch/master?svg=true)](https://ci.appveyor.com/project/wang-boyu/qssh/branch/master) [![License: LGPL v2](https://img.shields.io/badge/License-LGPL%20v2-blue.svg)](LICENSE.LGPL)
---

QSsh provides SSH and SFTP support for Qt applications. The aim of this project is to provide an easy way to use these protocols in any Qt application.

This project is based on Qt Creator's libQtcSsh.so. All the credits to Qt Creator's team!

### Prerequisites

- Qt 5.3 or later
- If to build with CMake (3.6 or later):
  - On Linux: g++ 4.8 or later, or clang++ 3.6 or later
  - On Mac: Xcode 6.4 or later
  - On Windows: *to be updated*
  - Qt5 installation prefix should be added into `CMAKE_PREFIX_PATH`

### Compiling QSsh

- CMake

```bash
$ cmake -H. -Bbuild
$ cmake --build build -- -j4
```

- qmake

```bash
$ mkdir build
$ cd build
$ qmake $SOURCE_DIRECTORY/qssh.pro
$ make (or mingw32-make or nmake depending on your platform)
```

- or you can open `qssh.pro` with Qt Creator

### Examples

- *to be updated*
