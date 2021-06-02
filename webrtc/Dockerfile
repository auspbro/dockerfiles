################################
#
# Base image centos 7.6.1810

FROM centos:7.6.1810
LABEL Description="This is the complete image for WebRTC360 CentOS 7.6"
LABEL Vendor="Intel Corporation"
WORKDIR /root

ARG NODE_VER=v10.21.0
ARG NODE_REPO=https://nodejs.org/dist/${NODE_VER}/node-${NODE_VER}-linux-x64.tar.xz

COPY scripts/mongodb-org-4.4.repo /etc/yum.repos.d/

# Prerequisites
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 && \
    yum install -y ca-certificates wget xz-utils && \
    yum install -y epel-release boost-system boost-thread log4cxx glib2 freetype-devel psmisc && \
    yum install -y rabbitmq-server && \
    yum install -y mongodb-org

RUN source ~/.bashrc && \
    wget ${NODE_REPO} && \
    tar xf node-${NODE_VER}-linux-x64.tar.xz && \
    cp node-*/* /usr/local -rf && rm -rf node-* && \
    rm -rf /var/cache/yum/*

RUN mkdir -pv /root/owt-server/dist && \
    mkdir -pv /root/owt-server/build/libdeps/build

COPY rest/ /root/owt-server/rest/
COPY dist/ /root/owt-server/dist/
COPY build/ /root/owt-server/build/
COPY deploy/test1_h265_3840x2048_30fps_30M_200frames.mp4 /root/4k.mp4

RUN cd /root/owt-server/rest/scripts/ && \
    npm install

COPY deploy/systemctl.py /usr/bin/systemctl
RUN chmod a+x /usr/bin/systemctl

ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/root/owt-server/build/libdeps/build/lib
ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/root/owt-server/build/libdeps/build/lib64:/usr/local/lib
