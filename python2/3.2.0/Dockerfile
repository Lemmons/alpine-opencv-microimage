#1 from base alpine
FROM alpine:3.5

#2 Add Edge and bleeding repos
# add the edge repositories
RUN echo "@edge-testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    echo "@edge-community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

#3 update apk, install dependencies, build opencv, cleanup
RUN apk update \
 && apk upgrade \
 && apk add --no-cache \
        build-base \
        clang \
        clang-dev \
        cmake \
        git \
        pkgconf \
        wget \
        libtbb@edge-testing \
        libtbb-dev@edge-testing \
        libjpeg \
        libjpeg-turbo-dev \
        libpng \
        libpng-dev \
        libwebp \
        libwebp-dev \
        tiff \
        tiff-dev \
        libjasper \
        jasper-dev \
        tesseract-ocr \
        tesseract-ocr-dev \
        leptonica \
        leptonica-dev \
        python \
        python-dev \
        py-numpy@edge-community \
        py-numpy-dev@edge-community \
        linux-headers\
 && cd /tmp \
 && wget -O opencv-3.2.0.tar.gz https://github.com/opencv/opencv/archive/3.2.0.tar.gz \
 && wget -O opencv_contrib-3.2.0.tar.gz https://github.com/opencv/opencv_contrib/archive/3.2.0.tar.gz \
 && tar -xzf opencv-3.2.0.tar.gz \
 && tar -xzf opencv_contrib-3.2.0.tar.gz \
 && cd /tmp/opencv-3.2.0 \
 && mkdir build \
 && cd build \
 && CC=/usr/bin/clang CXX=/usr/bin/clang++ cmake \
    -D OPENCV_EXTRA_MODULES_PATH=/tmp/opencv_contrib-3.2.0/modules \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr \
    -D WITH_FFMPEG=NO \
    -D WITH_IPP=NO \
    -D WITH_OPENEXR=NO \
    -D WITH_TBB=YES \
    -D WITH_1394=NO \
    -D BUILD_PERF_TESTS=OFF \
    -D BUILD_TESTS=OFF .. \
&& make -j2 \
&& make install \
&& cd / \
&& rm -rf /tmp/opencv-3.2.0* /tmp/opencv_contrib-3.2.0* \
&& apk del \
      build-base \
      clang \
      clang-dev \
      cmake \
      git \
      pkgconf \
      wget \
      libtbb-dev \
      libjpeg-turbo-dev \
      libpng-dev \
      tiff-dev \
      jasper-dev \
      tesseract-ocr-dev \
      leptonica-dev \
      python-dev \
      py-numpy-dev
