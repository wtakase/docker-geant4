FROM wtakase/geant4-base
MAINTAINER wtakase <wataru.takase@kek.jp>

ENV GEANT4_VERSION 10.01.p02
RUN mkdir -p /opt/geant4/{src,build} && \
    curl -o /opt/geant4/geant4.${GEANT4_VERSION}.tar.gz \
            http://geant4.cern.ch/support/source/geant4.${GEANT4_VERSION}.tar.gz && \
    tar zxf /opt/geant4/geant4.${GEANT4_VERSION}.tar.gz -C /opt/geant4/src && \
    rm -f /opt/geant4/geant4.${GEANT4_VERSION}.tar.gz && \
    cd /opt/geant4/build && \
    cmake -DGEANT4_INSTALL_DATA=on \
          -DGEANT4_USE_OPENGL_X11=on \
          -DGEANT4_USE_QT=on \
          -DCMAKE_INSTALL_PREFIX=../ \
          ../src/geant4.${GEANT4_VERSION} && \
    make -j`grep -c processor /proc/cpuinfo` && \
    make install && \
    rm -rf /opt/geant4/{src,build}
