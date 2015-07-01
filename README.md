YUnix
=====

Yorick plug-in to access low level i/o Unix functions like `open`, `ioctl`,
etc.

Names
-----
As a general rule, the names of the functions provided by the plug-in are
the name of the corresponding functions in the C library prefixed by `unx_`.
Similarly, the names of the macros and constants are prefixed by `UNX_`.

For instance:
```C
#include "unix.i"
f = unx_open(filename, UNX_O_RDONLY)
loc = unx_lseek(l, off, UNX_SEEK_CUR);
```

Error Management
----------------

Dealing with errors depends whether a low level routine is called as a
Yorick function or as a Yorick subroutine:

* When called as a **Yorick function**, the returned value is the same at
  the one returned by the C counterpart.  Most low-level C functions return
  a value which can be used to figure out whether an error occured.  For
  instance `0` in case of success and `-1` in case of failure.  It is the
  responsability of the caller to check the returned value.  If an error
  occured, the function `unx_errno` can be called to retrieve the last
  error code and the function `unx_strerror` can be used to get an
  explanatory message about the last error code or a given error code.

* When called as a **Yorick subroutine**, any returned value is discarded,
  thus the implementation will throw an error whenever an error occured.

In any case, when an error occurs at the Yorick level (*e.g.*, a string
argument is provided whereas an integer is expected), an error is thrown.


Installation
------------

In short, building and installing the plug-in can be as quick as:
````
$ cd $BUILD_DIR
$ $SRC_DIR/configure
$ make
$ make install
````
where `$BUILD_DIR` is the build directory (at your convenience) and
`$SRC\_DIR` is the source directory of the plug-in code.  The build and
source directories can be the same in which case, call `./configure` to
configure for building.

Then, to use the plug-in in Yorick:
````
$ yorick
> include "sox.i"
````
More detailled explanations are given below.

1. You must have Yorick and the SoX library installed on your machine.

2. Unpack the plug-in code somewhere.

3. Configure for compilation.  The are two possibilities:

   For an **in-place build**, go to the source directory of the plug-in
   code and run the configuration script:
   ````
   $ cd SRC_DIR
   $ ./configure
   ````
   To see the configuration options, call:
   ````
   $ ./configure --help
   ````

   To compile in a **different build directory**, say BUILD_DIR, create the
   build directory, go to the build directory, and run the configuration
   script:
   ````
   $ mkdir -p $BUILD_DIR
   $ cd $BUILD_DIR
   $ $SRC_DIR/configure
   ````
   where `$SRC_DIR` is the path to the source directory of the plug-in
   code. To see the configuration options, call:
   ````
   $ $SRC_DIR/configure --help
   ````

4. Compile the code:
   ````
   $ make
   ````

4. Install the plug-in in Yorick directories:
   ````
   $ make install
   ````

