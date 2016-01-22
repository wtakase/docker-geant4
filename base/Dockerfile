FROM centos:7
MAINTAINER wtakase <wataru.takase@kek.jp>

ENV ROOT_VERSION 5.34.34

RUN yum update -y
RUN yum install -y gcc-c++ tar expat-devel libXmu-devel libXt-devel \
                   freeglut-devel qt-devel cmake make libX11-devel \
                   libXpm-devel libXft-devel libXext-devel

RUN echo ". /opt/geant4/bin/geant4.sh" > /etc/profile.d/geant4.sh
ENV HOME /root
WORKDIR /root

RUN mkdir -p /opt/root/{src,build} && \
    curl -o /opt/root/root_v${ROOT_VERSION}.source.tar.gz \
            https://root.cern.ch/download/root_v${ROOT_VERSION}.source.tar.gz && \
    tar zxf /opt/root/root_v${ROOT_VERSION}.source.tar.gz -C /opt/root/src && \
    rm -f /opt/root/root_v${ROOT_VERSION}.source.tar.gz && \
    cd /opt/root/build && \
    cmake -DCMAKE_INSTALL_PREFIX=../ ../src/root && \
    make -j`grep -c processor /proc/cpuinfo` && \
    make install && \
    echo ". /opt/root/bin/thisroot.sh" > /etc/profile.d/root.sh && \
    rm -rf /opt/root/{src,build}
