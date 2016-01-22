FROM wtakase/geant4-data:10.2
MAINTAINER wtakase <wataru.takase@kek.jp>

RUN cd /opt/geant4/build && \
    cmake -DGEANT4_USE_OPENGL_X11=on \
          -DGEANT4_USE_QT=on \
          -DCMAKE_INSTALL_PREFIX=../ \
          ../src/geant4 && \
    make -j`grep -c processor /proc/cpuinfo` && \
    make install && \
    rm -rf /opt/geant4/{src,build}
