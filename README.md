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

Tencent O266dec plugin (0.0.1)
=========================================================================

Tencent O266dec plugin is a plugin for VLC player that enables VLC to play H.266
Annex B bit streams.

Reference:
"Performance of a VVC software decoder," B. Zhu, S. Liu, X. Xu, X. Zhang, C. Gu, L. Wang, W. Feng, JVET-T0095


Build instructions (macOS):

Please install th266dec in '/usr/local' directory. This is the default if it is build from source (on macOS).

Build commands for macOS:
mkdir build
cd build
JDK_HOME="" ../extras/package/macosx/build.sh -c -j 4

This build commands have been tested on macOS 10.15.6, Xcode version 11.6 (11E708).
More information can be found at https://wiki.videolan.org/MacOSCompile.
Build on other platforms may be possible but has not been tested.

Note:
The build process will download and build the dependencies from source, which takes a long time.

Play raw VVC video stream on macOS:
For example, the input is input.bin at 50fps.
./build/bin/vlc-osx-static input.bin --no-drop-late-frames --avformat-fps=50

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
