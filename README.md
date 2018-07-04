# gdl_native_windows_build

Welcome visitor. This repository is created to make possible to build [gnudatalanguage](https://github.com/gnudatalanguage/gdl) without any serious flaws on Windows. I use Windows 10 64 bit right now, so this will be the main OS to test on. But any experience with other Windows versions are welcome.
As of now, I use [CMake](https://cmake.org/) to build the projects and [vcpkg](https://github.com/Microsoft/vcpkg) to handle the requirements.

# How to build GDL on Windows using CMAKE and VisualStudio 2017

To build GDL on Windows (natively), you have to make the following steps (as of 2018. 07. 02 with GDL and WinEditLine)

1. Make a wineditline_build directory next to your wineditline (git source as of now: https://github.com/Csega/wineditline --> pull request made to the upstream, but no response yet).
2. Navigate to the wineditline_build directory and give the following two commands:
3. cmake -DCMAKE_INSTALL_PREFIX=D:\prog\github\wineditline_install ..\wineditline\
4. cmake --build . --config Release --target install
5. After these commands finished successfully, navigate to the gdl_build library (put next to your GDL git source library -- also available under github.com/Csega as of now, pull request made), and give the following command:
6. cmake -DEDITLINEDIR=D:\Prog\GitHub\wineditline_install ..\gdl\

This should find your compiled Editline directory and *should* complain about not finding ZLIB. This is a work in progress.

# Using [vcpkg](https://github.com/Microsoft/vcpkg) for building and installing the prerequisites

1. First you have to build the necessary (and available) prerequisites, which are (as of 2018. July 4.):
  * pdcurses
  * zlib
  * gsl
  * plplot[wxwidgets] (with WXWidgets support)
  * graphicsmagick
  * wxwidgets
  * netcdf-c
  * hdf5
  * fftw3
  * proj4
  * eigen3

2. You have to give the following command (and wait a bit) in vcpkg (after pulling vcpkg, and run the .\bootstrap-vcpkg.bat):
.\vcpkg.exe install pdcurses:x86-windows zlib:x86-windows gsl:x86-windows plplot[core,wxwidgets]:x86-windows graphicsmagick:x86-windows wxwidgets:x86-windows netcdf-c:x86-windows hdf5:x86-windows fftw3:x86-windows proj4:x86-windows eigen3:x86-windows

# TODOs

1. GDL CMakeLists.txt: set(CMAKE_PREFIX_PATH ${NCURSESDIR}) --> set(CMAKE_PREFIX_PATH ${CMAKE_PREFIX_PATH} ${NCURSESDIR}) etc. --> Done, but it caused some [disagreement](https://github.com/gnudatalanguage/gdl/pull/416) in the development team, so maybe other solutions will be necessary to implement.
2. Make available WinEditLine as a vcpkg package.
3. Figure out how to use vcpkg toolchain file with the suggested solutions at the GDL community (CMAKE_SYSTEM_PREFIX_PATH instead of CMAKE_PREFIX_PATH).