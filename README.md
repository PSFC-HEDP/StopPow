General Information
===================

This is the charged-particle stopping power (StopPow) library.

This is an object-oriented library which implements several models
for charged-particle stopping power in various materials.

## File structure

There are several directories in this package, which contain:

- [`doc/`](doc/): Doxygen-generated documentation (html/tex)
- [`examples/`](examples/): Simple code examples for C++, Java, Python for using the library. Latter two require native-built libraries
- [`java_swig/`](java_swig/): SWIG wrapper and makefile for generating java JNI library for your platform
- [`lib/`](lib/): makefile for generated shared library file (so/dll) for your platform
- [`python_swig/`](python_swig/): SWIG wrapper and makefile for generating python library.
- [`src/`](src/): the source files
- [`StopPowGUI/`](StopPowGUI/): NetBeans project folder for a Java front end to the library
- [`test/`](test/): A variety of test cases

## Installation

Note on make:
This package heavily uses GNU make style makefiles.
The ones for lib/ and examples/c++ have been tested as working on Mac OS X, Linux, and Windows (mingw).
Makefiles for Python and Java wrappers only tested on OS X so far.

### Requirements

System requirements:
- C++ compiler with C++11 support
- GSL 1.15 or 1.16
- GNU make or similar

For the SWIG libraries:
- SWIG
- Java 7 JDK / JRE
- Python with headers

For the documentation:
- Doxygen

This code relies heavily on the GNU Scientific Library (GSL).
Before you do anything else you'll need to install GSL 1.15 or 1.16 (it must be one of those two versions).
On Linux this is pretty straightforward.
[Download the source](https://www.gnu.org/software/gsl/#downloading) and then run the following:
~~~bash
tar --extract --file gsl-1.16.tar.gz
cd gsl-1.16/
./configure
make
make install
~~~

The Makefile generates a shared object file for GSL but doesn't necessarily make it findable by C.
You'll need to update your `LD_LIBRARY_PATH` to include th directory where it got installed.
Run the following command and/or add it to your `~/.bashrc` file:
~~~bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib/
~~~

Justin has also installed GSL on Windows but he lost his notes and can't remember how he did it and also apparently deleted all of the intermediate files.
He's very sorry about that.
He thinks he downloaded a partially precompiled copy of GSL 1.16 (and maybe some other GNU source files) from the internet but he can't find that particular wobsite anymore.
He might have used MinGW's GCC and GNUWin32's Make?
You'll probably need to create an environment variable called `C_INCLUDE_PATH` and set it to the downloaded directory.
Don't use Vcpkg, as it only has GSL versions 2.3+.

### Building as C library

If you just want to use this project as a C library, all you need to do is run the makefile in [`lib/`](lib/):
~~~bash
cd StopPow/lib/
make
~~~

Ignore the deprecation warnings; it's fine.

### Building as Python library

It is also set up using the power of SWIG to function as a Python or Java library.
First you'll need to install SWIG, which depends on PCRE2.
[Download the PCRE2 source](https://github.com/PCRE2Project/pcre2/tags) (I tested this with version 10.43), then run the following:
~~~bash
tar --extract --file pcre2-10.43.tar.bz2
cd pcre2-10.43/
./configure
make
make install
~~~

Then, [download the SWIG source](https://www.swig.org/download.html) (I tested this with version 4.2.1), then run the following:
~~~bash
tar --extract --file swig-4.2.1.tar.gz
cd swig-4.2.1/
./configure
make
make install
~~~

Finally, build the Python library:
~~~bash
cd StopPow/python_swig/
make
~~~

This creates a new directory called `dist/` containing a `.py` file and a `.so` file; move both to the sources folder of whatever project in wich you want to use this.
You can import all the functionality from the Python file, which will automatically pull all the functionality from the shared object file.
Graeme claimed there was a `main.py` script that he also had to run, but as far as Justin and Joe can tell that file doesn't exist, so he probably just accidentally downloaded a virus somewhere.

Again, Justin has done this all on Windows but doesn't remember how.
He definitely used the Visual Studio Build Tools.
He ran some commands in "Developer Command Prompt for VS 2019", which resulted in a file called `_StopPow.lib`,
which he then somehow turned into `_StopPow.cp39-win_amd64.pyc`.
And that's the file from which `StopPow.py` pulls its functionality
(interestingly, even tho it has "p39" in the name, it also works with Python 3.10).

Don't run `setup.py`; it references files that don't exist, so it's unclear if it was ever tested.
Also, it uses Distutils, which is apparently getting removed in Python 3.12.
Thanks software developers, I'm so glad you understand that everyone continuously develops all of their code just like you do so that removing previously available functionality in a dependency of a dependency of my code isn't an inconvenience at all!

### Building as Java library

Building this for Java is probably similar to building it for Python.
But why would you use Java in this day and age when you could be using Rust?

### Building the documentation

If you want to read the nicely-formatted API and you're on Linux, you can do so with Doxygen.
Install it from APT (or whatever packaging tool your system uses) and then run the build script:
~~~bash
apt install doxygen
cd StopPow/doc/
./generate_doc.sh
~~~

If you're not on Linux, you're not allowed to read the API.

### Other

There is also a GUI app, but since Alex never explained how to use it, it's unlikely anyone ever will.

There are also tests but they fail for Justin even tho everything else is working correctly, so.

## Usage

The documentation doesn't provide much by way of explaining how to use this library, but please peruse the examples in [`examples/`](examples/).
