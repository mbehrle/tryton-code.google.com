#summary How to install build installer packages for Windows



<font color='darkred' size='larger'>This page is intended for those who want to build Windows installer packages. This is the task of software deployment. For those of you who just want to <i>use</i> Tryton, simply follow the instructions for <a href='InstallationWindows.md'>installing Tryton on Windows</a>.</font> (Note: At this time, instructions are only provided for packaging the Windows client.)

# Building a Windows Client Installer #

## Setup pyGTK environment ##

  1. Install [pygtk-all-in-one](http://ftp.gnome.org/pub/GNOME/binaries/win32/pygtk/2.24/)
  1. Install tryton dependencies using `pip`
  1. Install [Nullsoft Scriptable Install System](http://nsis.sourceforge.net/Main_Page)
  1. Fetch the tryton source code

## Running the Client ##

  1. Execute using
```
python bin/tryton
```

## Packaging the Client ##

  1. Copy `msvcr90.dll`, `msvcp90.dll` and `msvcm90.dll` in the main tryton directory.
  1. Run py2exe
```
python setup.py py2exe
```
  1. The setup is built.