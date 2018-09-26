OpenRISC 1000 Toolchain
=======================

This repository contains a single release, that of:

  * or1k-linux-musl-4.9.1: The OpenRISC 1000 toolchain, prebuilt for amd64. Includes gcc 4.9.1.

This file was originally downloaded from [lis.ei.tum.de](http://lis.ei.tum.de/pub-download/openrisc-builds/or1k-linux-musl/), and is the same version of GCC used to build software for [jor1k](https://github.com/s-macke/jor1k).


Why?
----

Attempting to locate the version of GCC used in the [jor1k](https://github.com/s-macke/jor1k) project is a difficult task. Most links are for much more recent versions of the toolchain.

Applications compiled in more recent toolchains must be compiled statically, as the runtime supplied by jor1k is using an older version.

Using the toolchain in this release allows for non-static compilation of applications which can be run on the jor1k emulator. This results in smaller programs, by several margins. A statically compiled C++ program with a recent toolset (5.3.0) results in a file of a megabyte or more, compared to approximately 100k (or smaller) for a reasonably complex program compiled non-statically with this toolchain.


Target
------

This toolchain was built for Ubuntu 14.04 on amd64 (x86_64). However, as of writing (2018) this toolchain works without modification on Ubuntu 18.04 (LTS).

It is intended for developers of OpenRISC software that would like to target the [jor1k](https://github.com/s-macke/jor1k) emulator. Code written for standards compliant C++ (eg, C++14) should work without modification on both the x86_64 platform and OpenRISC.


Prequisites
-----------

The following libraries are known to be required, and may require some further tweaking:

  * libmpfr6
    
    Can be installed using `sudo apt install libmpfr6`. If `or1k-linux-musl-cc1` reports an error loading `libmpfr.so.4`, the following should fix it:
    
    ```
    cd /usr/lib/x86_64-linux-gnu
    sudo ln -s libmpfr.so.6 libmpfr.so.4
    ```
    
Using
-----

Typically, the files in this archive are extracted to a directory under `/opt`, but it can be anywhere you prefer. That path needs to be added to your `PATH` environment. The naming convention of the tools is:

   or1k-linux-musl-**application**

Where **aplication** is one of `gcc`, `g++`, etc. The standard applications available as of GCC 4.9.1 should be present.

When using a Makefile that allows a custom compiler, the following `Makefile` environment variables can often be overridden:

  * `CC=or1k-linux-musl-gcc`

  * `CXX=or1k-linux-musl-g++`

Example:

```
make CONF=Release CC=or1k-linux-musl-gcc CXX-or1k-linux-musl-g++
```
