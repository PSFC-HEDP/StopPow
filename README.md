General Information
===================

This is the charged-particle stopping power (StopPow) library.

This is an object-oriented library which implements several models
for charged-particle stopping power in various materials.

There are several directories in this package, which contain:

doc: Doxygen-generated documentation (html/tex)
examples: Simple code examples for C++, Java, Python for using the library. Latter two require native-built libraries
java_swig: SWIG wrapper and makefile for generating java JNI library for your platform
lib: makefile for generated shared library file (so/dll) for your platform
python_swig: SWIG wrapper and makefile for generating python library.
src: the source files
StopPowGUI: NetBeans project folder for a Java front end to the library
test: A variety of test cases

Note on make:
This package heavily uses GNU make style makefiles.
The ones for lib/ and examples/c++ have been tested as working on Mac OS X, Linux, and Windows (mingw).
Makefiles for Python and Java wrappers only tested on OS X so far.

System requirements:
- C++ compiler with C++11 support
- GSL libraries (http://www.gnu.org/software/gsl/)
- GNU make or similar
- Doxygen
For the SWIG libraries:
- SWIG v2.x
- Java 7 JDK / JRE
- Python with headers

## Installation suggestions (in connection with NIF_WRF)
- get gsl version 1.x (not 2.x)
    - ./configure
    - make
    - make check
    - make install
- get swig (tested with v 3.something)
- get WRF_Analysis
- get StopPow, build library and :
    - get stoppow from github
    - cd python_swig, make
    - move _StopPow.so AND StopPow.py to WRF_Analysis/util/
- run WRF:
    - move main.py to WRF_Analysis-master (ie WRF_Analysis/../)
    - python3 main.py
