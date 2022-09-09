# teamspeak-plugin-ducker

### Ducking
Global Ducking: Reduce the volume of musicbots when someone talks.

Channel Ducking: Reduce the volume of home or foreing tabs when someone talks on the other one or you receive a whisper.

![Channel Ducking](https://github.com/thorwe/CrossTalk/raw/master/misc/ct_screenie_duck.png "Channel Ducking")

## Installation

It is recommended to install the plugin directly from within the client, so that it gets automatically updated.
In you TeamSpeak client, go to Tools->Options->Addons->Browse, search for the "Ducker" plugin and install.

## Compiling yourself
After cloning, you'll have to manually initialize the submodules:
```
git submodule update --init --recursive
```

Qt in the minor version of the client is required, e.g.

Compilation instructions between Linux and Windows are a different, check the correct sections below:\

### Windows
```cmd
mkdir build32 & pushd build32
cmake -G "Visual Studio 16 2019" -A Win32 -DCMAKE_PREFIX_PATH="path_to/Qt/5.12.3/msvc2017" ..
popd
mkdir build64 & pushd build64
cmake -G "Visual Studio 16 2019" -A x64  -DCMAKE_PREFIX_PATH="path_to/Qt/5.12.3/msvc2017_64" ..
```
### Linux
Thanks to Nithanim's [gist](https://gist.github.com/Nithanim/3f65a2a7631373c445c7998a25f7fad6) we have compilation
instructions for Linux.
```bash
mkdir build32 && pushd build32
cmake ..
make
mkdir build64 && pushd build64
cmake ..
make
```
It might be the case that the `CTRL + L` logs of TS mention an error with the ducker plugin regarding the wrong QT version.
In that case your system QT may be wrong. To fix this issue, look for a mention of TS3's QT version and download that from
the [QT download repo](https://download.qt.io/official_releases/qt/5.12/5.12.1/).
Besides that, add the following lines to the top of the root repo's [CMakeLists.txt](CMakeLists.txt):
```cmake
set(Qt5Core_DIR "~/qt/Qt5.12.1/5.12.1/gcc_64/lib/cmake/Qt5Core/")
set(Qt5_DIR "~/qt/Qt5.12.1/5.12.1/gcc_64/lib/cmake/Qt5/")
set(QT_QMAKE_EXECUTABLE "~/qt/Qt5.12.1/5.12.1/gcc_64/bin/qmake")
```
In case of errors mentioning `fpermissive`, add this line to [CMakeLists.txt](deps/teamspeak-plugin-qt-common/CMakeLists.txt):
```cmake
set(CMAKE_CXX_FLAGS "-fpermissive")
```