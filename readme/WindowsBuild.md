# Xournal++ Windows Build



## Preparation
1. Install [MSYS2](https://www.msys2.org/) to a short path without spaces.
2. Install [NSIS](https://nsis.sourceforge.io/Download) to the standard directory.
3. Start Mingw-w32 32bit. (Always check if it says **MINGW32** - not 64bit and not MSYS2)

This will open a console. All following steps happen in this console.

## Update MSYS2

Do this multiple times, close the Terminal after each update
```bash
pacman -Syuu
```

## Install GIT

```bash
pacman -S git
```

## Install Build tools

```bash
pacman -S mingw-w64-i686-toolchain \
          mingw-w64-i686-cmake \
          mingw-w64-i686-make \
          mingw-w64-i686-ninja \
          patch \
          make \
          tar \
          mingw-w64-i686-cppunit
```
note that its -i686- and not -x86_64-

-> press enter multiple times / confirm all default values

## Install dependencies

```bash
pacman -S mingw-w64-i686-poppler \
          mingw-w64-i686-gtk3 \
          mingw-w64-i686-libsndfile \
          mingw-w64-i686-libzip
```
-> press enter multiple times / confirm all default values

## Get sources

```bash
git clone https://github.com/xournalpp/xournalpp.git
cd xournalpp/
```

## Install sndfile / PortAudio

Build/Install portaudio with
```bash
windows-setup/build-portaudio.sh
```

### Install Lua

Build/Install lua with ( please note that this file is changed from the 64bit one)
```bash
windows-setup/build-lua.sh
```

## Build Xournal++

```bash
mkdir build
cd build/
cmake ..
cmake --build .
```

You can run Xournal++ with
```bash
./src/xournalpp.exe
```
or package it in an installer (see below).

## Packaging and Setup
Create the installer with
```bash
windows-setup/build-setup.sh
```

The installer will be located at `windows-setup/xournalpp-setup.exe`
