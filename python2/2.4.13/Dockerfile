#1 from base alpine
FROM alpine:3.5

#2 Add Edge and bleeding repos
# add the edge repositories
RUN echo "@edge-testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    echo "@edge-community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

#3 upgrade System
RUN apk update && apk upgrade

#4
RUN apk add --update \
  python \
  python-dev \
  make \
  cmake \
  gcc \
  g++ \
  git \
  pkgconf \
  unzip \
  wget \
  py-pip \
  build-base \
  gsl \
  libavc1394-dev  \
  libtbb@edge-testing  \
  libtbb-dev@edge-testing   \
  libjpeg  \
  libjpeg-turbo-dev \
  libpng-dev \
  libjasper \
  libdc1394-dev \
  clang-dev \
  clang \
  tiff-dev \
  libwebp-dev \
  py-numpy-dev@edge-community \
  py-scipy-dev@edge-testing \
  openblas-dev@edge-community \
  linux-headers

#5 defining compilers
ENV CC /usr/bin/clang
ENV CXX /usr/bin/clang++

#6 patch sysctl issue
ADD 2.4.13.patch /tmp/

#7 opencv 2.4
RUN mkdir /opt && cd /opt && \
  wget https://github.com/opencv/opencv/archive/2.4.13.zip && \
  unzip 2.4.13.zip && \
  cd /opt/opencv-2.4.13 && \
  patch -p1 < /tmp/2.4.13.patch && \
  mkdir build && \
  cd build && \
  cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_FFMPEG=NO \
  -D WITH_IPP=NO -D WITH_OPENEXR=NO .. && \
  make VERBOSE=1 && \
  make && \
  make install


#8 Clean APK cache
RUN rm -rf /var/cache/apk/*
