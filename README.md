This is an attempt at 32bit version of the xournalpp, for the original one please check out https://github.com/xournalpp/xournalpp/

# Current progress

Thanks to [andreasb242](https://github.com/andreasb242) I have been able to do the following.

Follow build setup from [here](https://github.com/iamashwin99/xournalpp/blob/master/readme/WindowsBuild.md)
or as follows:

## Preparation
1. Install [MSYS2](https://www.msys2.org/) to a short path without spaces.
2. Install [NSIS](https://nsis.sourceforge.io/Download) to the standard directory.
3. Start **Mingw-w32 32bit**. (Always check if it says **MINGW32** - not 64bit and not MSYS2)

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

## Install Build tools (updated toolchain and cmake)

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
**note that its -i686- and not -x86_64-**

-> press enter multiple times / confirm all default values

## Install dependencies

```bash
pacman -S mingw-w64-i686-poppler \
          mingw-w64-i686-gtk3 \
          mingw-w64-i686-libsndfile \
          mingw-w64-i686-libzip
```
-> press enter multiple times / confirm all default values
**note that its -i686- and not -x86_64-**

## Get sources

```bash
git clone https://github.com/xournalpp/xournalpp.git
cd xournalpp/
```
## Mod the source
modify the build-lua.sh to the one [here](https://github.com/iamashwin99/xournalpp/blob/master/windows-setup/build-lua.sh)

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
In this process you may get some warning but the make should complete with no error. 
Take a look at my terminal out put for the build [here](http://p.ip.fi/2RXt)



You can run Xournal++ with
```bash
./src/xournalpp.exe
```
At this point, the executable does work but the display area is not shown
see this [image](https://imgur.com/noFtPxh)

from line 422 onwards of my [terminal output](http://p.ip.fi/2RXt) you can see a bunch of warnings but im not sure if any of those correspond to the display area problem..

I hope some developer of xournalpp can take a look at it to help me sort out the issue.
