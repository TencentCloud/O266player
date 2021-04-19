Tencent O266dec decoder library (0.0.1)
=========================================================================

Tencent Media Lab's O266 decoder is a high performance CPU-efficient
H.266/VVC decoder library (O266dec) designed to be integrated into player and
transcoding applications. The decoder library can be used to play back
H.266 Annex B bitstreams and is available to try on your target
platforms using the modified VLC player available at our Github page
here: https://github.com/TencentCloud/O266player

To enable VLC player to recognize H.266 bitstream input, a modified
VLC player was created.  The source code for the modified VLC player
is available in the O266player Github repository. The required decoder
library file is available as a binary only from Tencent and is limited
to 600 frames of decode for evaluation purposes.

For GPL compliance, the decoder library binary is not distributed on the 
GitHub page and instead is hosted in the Resources section of 
the Tencent Media Lab website:  https://multimedia.tencent.com

Reference:
"Performance of a VVC software decoder," B. Zhu, S. Liu, X. Xu, X. Zhang, C. Gu, L. Wang, W. Feng, JVET-T0095

README for the VLC media player
===============================

VLC is a popular libre and open source media player and multimedia engine,
used by a large number of individuals, professionals, companies and
institutions. Using open source technologies and libraries, VLC has been
ported to most computing platforms, including GNU/Linux, Windows, Mac OS X,
BSD, iOS and Android.
VLC can play most multimedia files, discs, streams, allows playback from
devices, and is able to convert to or stream in various formats.
The VideoLAN project was started at the university École Centrale Paris who
relicensed VLC under the GPLv2 license in February 2001. Since then, VLC has
been downloaded close to one billion times.

Build Instructions
==================

Below are the instructions for macOS and Windows builds. Build on other platforms is possible but has not been tested.

Build instructions (macOS):
---------------------------
Please install libo266dec in '/usr/local' directory. This can be done by extracting the decoder package and running the install script.
```sh
sudo ./install.sh
```

Build commands for macOS:
```
mkdir build
cd build
JDK_HOME="" PKG_CONFIG_LIBDIR="/usr/local/lib/pkgconfig:$PWD/../extras/tools/build/lib/pkgconfig" ../extras/package/macosx/build.sh -c -j 4
```

This build commands have been tested on macOS 10.15.6, Xcode version 11.6 (11E708).

More information can be found at https://wiki.videolan.org/MacOSCompile.

Build instructions (Windows):
-----------------------------
Windows build requires cross-compiling from Linux environment using docker. A docker file is provided in "docker" directory.

To install docker on Windows, follow the instructions on https://docs.docker.com/docker-for-windows/install/

Build steps for Windows:
1. Download docker/Dockerfile. No need to manually fetching the entire repository. It will be fetched by the build script.
2. Rename the decoder package to o266dec-win64.tar.tz, and put it in the same folder as the downloaded Dockerfile. No need to uncompress it.
3. Go to the folder containing the decoder library and Dockerfile, run the following command
```
docker build -t o266player --force-rm .
```
4. After the build finishes, use following command to fetch the player package, then uncompress it and the player is ready to use.
```
docker run --rm o266player cat /O266player/win32/vlc-3.0.11.1-w64.zip > vlc-3.0.11.1-w64.zip
```

The player has been tested on Windows Server 2016. Other Windows platforms have not been tested.

More information can be found at: https://wiki.videolan.org/Win32Compile.


Note:
The build process will download and build the dependencies from source, which takes a long time. On macOS, it may take over 5GB of disk space. On Windows, it may take over 13GB of disk space.

Usage Instructions
------------------

The VLC player must be launched with specific parameters. After VLC player is launched, the VLC native file browser or drag and drop can be used to add more bitstreams to the player.
The --avformat-fps parameter is used to cap the frame rate for real-time playback.

To play raw VVC video stream on macOS:

For example, the input file is input.bin at 50fps.
```
./build/bin/vlc-osx-static input.bin --no-drop-late-frames --avformat-fps=50
```

To play raw VVC vidoe stream on Windows:

For example, the input file is input.bin at 50fps.
```
vlc.exe input.bin --no-drop-late-frames --avformat-fps=50
```

Links:
======

The VLC web site  . . . . . http://www.videolan.org/
Support . . . . . . . . . . http://www.videolan.org/support/
Forums  . . . . . . . . . . http://forum.videolan.org/
Wiki  . . . . . . . . . . . http://wiki.videolan.org/
The Developers site . . . . http://wiki.videolan.org/Developers_Corner
VLC hacking guide . . . . . http://wiki.videolan.org/Hacker_Guide
Bugtracker  . . . . . . . . http://trac.videolan.org/vlc/
The VideoLAN web site . . . http://www.videolan.org/

Source Code Content:
===================
ABOUT-NLS          - Notes on the Free Translation Project.
AUTHORS            - VLC authors.
COPYING            - The GPL license.
COPYING.LIB        - The LGPL license.
INSTALL            - Installation and building instructions.
NEWS               - Important modifications between the releases.
README             - This file.
THANKS             - VLC contributors.

bin/               - VLC binaries.
bindings/          - libVLC bindings to other languages.
compat/            - compatibility library for operating systems missing
                     essential functionalities.
contrib/           - Facilities for retrieving external libraries and building
                     them for systems that don't have the right versions.
doc/               - Miscellaneous documentation.
extras/analyser    - Code analyser and editor specific files.
extras/buildsystem - different buildsystems specific files.
extras/misc        - Files that don't fit in the other extras/ categories.
extras/package     - VLC packaging specific files such as spec files.
extras/tools/      - Facilities for retrieving external building tools needed
                     for systems that don't have the right versions.
include/           - Header files.
lib/               - libVLC source code.
modules/           - VLC plugins and modules. Most of the code is here.
po/                - VLC translations.
share/             - Common Resources files.
src/               - libvlccore source code.
test/              - testing system.
