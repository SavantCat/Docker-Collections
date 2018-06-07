
FROM nvidia/cuda:8.0-devel-ubuntu16.04

MAINTAINER Katsuyoshi Hotta <scanf@me.com>

RUN apt-get update && \
        apt-get install -y \
        nano \
        git \
        wget \
        unzip \
        pkg-config \
        cmake \
        cmake-curses-gui \
        build-essential \
        libjpeg-dev \
        libpng-dev \
        libtiff-dev \
        cimg-dev \
        libglm-dev \
        libthrust-dev \
        libeigen3-dev \
        libavutil-dev \
        libavformat-dev \
        libavcodec-dev \
        libavdevice-dev \
        libopencv-dev \
	&& apt-get clean

RUN ln -s /usr/local/cuda/lib64/libcudart.so /usr/lib/libcudart.so
WORKDIR ~/
RUN git clone https://github.com/saccadic/Obstruction-Free-Photography.git /home/Obstruction-Free-Photography && \
        cd /home/Obstruction-Free-Photography && \ 
        mkdir obj && \
        make -j4 canny canny_cpu flow warp lk ransac ransac_cpu interpolate gd gd_cpu generate_bgfg spatial_coherence && \
        make -j4 main main2
