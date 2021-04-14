FROM ubuntu:20.04

# install build tools
RUN apt-get update \
  && apt-get install -y --no-install-recommends software-properties-common \
  && add-apt-repository ppa:rock-core/qt4 \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
    gcc-mingw-w64-x86-64 g++-mingw-w64-x86-64 mingw-w64-tools \
    lua5.2 libtool automake autoconf autopoint make gettext pkg-config \
    qt4-dev-tools qt5-default git subversion cmake cvs \
    wine64-development-tools libwine-dev zip p7zip nsis bzip2 \
    yasm ragel ant default-jdk dos2unix \
    curl patch python3 \
    g++ gperf libltdl-dev meson nasm python unzip \
    bison flex \
    wine \
    wget \
  && add-apt-repository --remove ppa:rock-core/qt4 \
  && apt-get --purge autoremove -y software-properties-common \
  && rm -rf /var/lib/apt/lists/*

# fetch player source code
RUN git clone --depth=1 https://github.com/TencentCloud/O266player.git

# build protoc
RUN cd /O266player/extras/tools \
  && ./bootstrap \
  && make .protoc

# bootstrap dependencies
RUN mkdir -p O266player/contrib/win32 \
  && cd O266player/contrib/win32 \
  && ../bootstrap --host=x86_64-w64-mingw32 \
  && make fetch

# install O266 decoder
ADD o266dec-win64.tar.xz /
RUN cd o266dec-win64 \
  && ./install.sh \
  && update-alternatives --set x86_64-w64-mingw32-gcc /usr/bin/x86_64-w64-mingw32-gcc-posix \
  && update-alternatives --set x86_64-w64-mingw32-g++ /usr/bin/x86_64-w64-mingw32-g++-posix

# build dependencies
RUN cd /O266player/contrib/win32 \
  && PATH=/O266player/extras/tools/build/bin:$PATH make -j`nproc` \
  && rm -f ../i686-w64-mingw32/bin/moc ../i686-w64-mingw32/bin/uic ../i686-w64-mingw32/bin/rcc \
  && ln -sf x86_64-w64-mingw32 ../i686-w64-mingw32

# avoid static linking to libssp
RUN rm /usr/lib/gcc/x86_64-w64-mingw32/*-posix/libssp.dll.a

# bootstrap and configure player
RUN cd /O266player \
  && ./bootstrap \
  && mkdir win32 \
  && cd win32 \
  && PKG_CONFIG_LIBDIR=/usr/local/lib/pkgconfig:/O266player/contrib/x86_64-w64-mingw32/lib/pkgconfig ../extras/package/win32/configure.sh --host=x86_64-w64-mingw32 --build=x86_64-pc-linux-gnu

# build player
RUN cd /O266player/win32 \
  && PATH=/O266player/extras/tools/build/bin:$PATH make -j`nproc`

# build package
RUN ln -sf /usr/include/wine/wine/windows /usr/include/wine/windows \
  && cd /O266player/win32 \
  && LIBVLC_CFLAGS=-I/O266player/win32/_win32/include LIBVLC_LIBS="-L/O266player/win32/_win32/lib -lvlc" make package-win-strip -j`nproc` \
  && cp /usr/local/lib/libo266dec.dll vlc-*/ \
  && cp /usr/lib/gcc/x86_64-w64-mingw32/*-posix/libgcc_s_seh-1.dll vlc-*/ \
  && cp /usr/lib/gcc/x86_64-w64-mingw32/*-posix/libstdc++-6.dll vlc-*/ \
  && cp /usr/x86_64-w64-mingw32/lib/libwinpthread-1.dll vlc-*/ \
  && make package-win32-zip
