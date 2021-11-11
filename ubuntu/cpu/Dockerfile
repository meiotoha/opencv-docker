FROM ubuntu:18.04
LABEL maintainer "maplelolita@gmail.com"
ARG THREAD=8
ARG OPENCV_VERSION=4.5.4

RUN apt update && apt install -y build-essential wget curl git bzip2 python3 zlib1g-dev cmake \
    && rm -rf /var/lib/apt/lists/* \
    && cd /tmp \
    && wget -O opencv.tar.gz https://github.com/opencv/opencv/archive/refs/tags/${OPENCV_VERSION}.tar.gz \
    && tar -xf opencv.tar.gz \
    && rm opencv.tar.gz \
    && wget -O opencv_contrib.tar.gz https://github.com/opencv/opencv_contrib/archive/refs/tags/${OPENCV_VERSION}.tar.gz \
    && tar -xf opencv_contrib.tar.gz  \
    && rm opencv_contrib.tar.gz \ 
    && cd /tmp/opencv-${OPENCV_VERSION} && mkdir build && cd build \
    && cmake .. \
    -DCMAKE_INSTALL_PREFIX=/usr/local/ \
    -DCMAKE_BUILD_TYPE=Release \
    -DOPENCV_EXTRA_MODULES_PATH=/tmp/opencv_contrib-${OPENCV_VERSION}/modules \
    -DPYTHON_EXECUTABLE=/usr/bin/python3 \
    -DBUILD_TESTS=OFF \
    -DBUILD_PERF_TESTS=OFF \
    -DBUILD_EXAMPLES=OFF \
    -DBUILD_opencv_world=ON \
    -Djava_bindings_generator=OFF \
    -Djs_bindings_generator=OFF \
    -Dobjc_bindings_generator=OFF \
    -Dpython_bindings_generator=OFF \
    && make -j${THREAD} && make install \
    && cd /tmp \
    && rm -rf /tmp/opencv-${OPENCV_VERSION} \
    && rm -rf /tmp/opencv_contrib-${OPENCV_VERSION} 