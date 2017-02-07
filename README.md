# clinfo for Windows

This is a port of clinfo from Ubuntu/Debian/etc to Windows.

Instead of using GNU Make, the build process uses CMake, and the source code has been modified to work with Microsoft Visual Studio in addition to GCC.
I've tested building this project on Visual Studio 2015 (MSVC14) and GCC 6.2 (Ubuntu 16.04).
I have done no testing on macOS (pull requests appreciated!), though it should work there.

I do not port dlopen/dlsym/dlclose; you'll need a version of these for Windows.
I used https://github.com/dlfcn-win32/dlfcn-win32 to create the binary below.

## Bugs

### Unresolved symbol for `EnumProcessModules`

The CMake project does not build-as is on Windows.
You'll get an error about an unresolved symbol `EnumProcessModules`, which comes from Psapi.lib.
I've not been able to get CMake to find or link to this library, so once the project has been configured,
you need to open the project in Visual Studio, go to the linker settings, and manually add Psapi.lib as a dependency library.
Pull requests for fixing this are very much appreciated!

## Released binary

See the "Release" tab on GitHub.

Built with Visual Studio 2015. You'll need to download and install the [Visual C++ for Visual Studio 2015 runtime](https://www.microsoft.com/en-us/download/details.aspx?id=48145).

## Original README

A simple OpenCL application that enumerates all possible platform and
device properties. Inspired by AMD's program of the same name, it is
coded in pure C99 and it tries to output all possible information,
including that provided by platform-specific extensions, and not to
crash on platform-unsupported properties (e.g. 1.2 properties on 1.1
platforms).