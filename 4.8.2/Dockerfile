FROM ubuntu:22.04
ENV QT_LIBS=/usr/local/lib \
    QT_DIR=/usr/local/Qt4.8.2
WORKDIR /workspace 
ARG MAKE_PARALLEL_JOBS=4
RUN echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/ubuntu-archive-keyring.gpg] http://archive.ubuntu.com/ubuntu bionic main universe' >> /etc/apt/sources.list \
    && apt update -y \
    && apt install -y \
            gcc-4.8 \
            g++-4.8 \
            build-essential \
            libfontconfig1-dev \
            libfreetype6-dev \
            libx11-dev \
            libxcursor-dev \
            libxext-dev \
            libxfixes-dev \
            libxft-dev \
            libxi-dev \
            libxrandr-dev \
            libxrender-dev \
    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 60 --slave /usr/bin/g++ g++ /usr/bin/g++-4.8
    
ADD https://download.qt.io/new_archive/qt/4.8/4.8.2/qt-everywhere-opensource-src-4.8.2.tar.gz src.tar.gz
RUN tar -xvf src.tar.gz \
    && cd qt* \
    && yes | ./configure \
        --opensource \
        -shared \
        -prefix /usr/local/Qt4.8.2 \
        -libdir /usr/local/lib \ 
        -platform linux-g++-64 \
        -qt-zlib \
        -xmlpatterns \
        -no-libjpeg \
        -no-libpng \
        -no-libtiff \
        -no-libmng \
        -no-gif \
        -no-phonon \
        -no-phonon-backend \
        -no-openvg \
        -no-qt3support \
        -no-webkit \
        -no-multimedia \
        -no-javascript-jit \
        -no-audio-backend \
        -no-openssl \
        -no-script \
        -no-scripttools \
        -no-declarative \
        -no-declarative-debug \
        -no-gui \
        -no-svg \
        -no-nis \
        -no-cups \
        -no-iconv \
        -no-dbus \
        -no-gtkstyle \
        -no-opengl \
        -no-sm \
        -no-xshape \
        -no-xvideo \
        -no-xsync \
        -no-xinerama \
        -no-xcursor \
        -no-xfixes \
        -no-xrender \
        -no-mitshm \
        -no-fontconfig \
        -no-xinput \
        -no-xkb \
        -no-glib \
        -nomake demos \
        -nomake examples \
        -nomake tools \
        -nomake translations \
        -nomake docs
RUN cd qt* \
    && make -j $MAKE_PARALLEL_JOBS \
    && make install

FROM ubuntu:22.04
ENV QT_LIBS=/usr/local/lib \
    QT_DIR=/usr/local/Qt4.8.2 \
    PATH=/usr/local/Qt4.8.2/bin:$PATH 
    
COPY --from=0 $QT_DIR $QT_DIR
COPY --from=0 $QT_LIBS $QT_LIBS