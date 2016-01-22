FROM wtakase/geant4-base
MAINTAINER wtakase <wataru.takase@kek.jp>

ENV GEANT4_VERSION 10.02
RUN mkdir -p /opt/geant4/{src,build} && \
    curl -o /opt/geant4/geant4.${GEANT4_VERSION}.tar.gz \
            http://geant4.cern.ch/support/source/geant4.${GEANT4_VERSION}.tar.gz && \
    tar zxf /opt/geant4/geant4.${GEANT4_VERSION}.tar.gz -C /opt/geant4/src && \
    mv /opt/geant4/src/geant4.${GEANT4_VERSION} /opt/geant4/src/geant4 && \
    G4_VERSION=`awk '/__version__/{gsub(/[=|:\47]/, "", $2); print $2; exit}' /opt/geant4/src/geant4/environments/g4py/source/python3/__init__.py` && \
    mkdir -p /opt/geant4/share/Geant4-${G4_VERSION}/data/ && \
    for DATA in `echo "G4NDL G4EMLOW PhotonEvaporation RadioactiveDecay G4NEUTRONXS G4PII RealSurface G4SAIDDATA G4ABLA G4ENSDFSTATE"`; do \
        DATA_VERSION=`awk "/${DATA}/{getline; print \\$2; exit}" /opt/geant4/src/geant4/cmake/Modules/Geant4DatasetDefinitions.cmake`; \
        if [ "${DATA}" = "PhotonEvaporation" -o "${DATA}" = "RadioactiveDecay" ]; then DATA="G4${DATA}"; fi; \
        curl -o /opt/geant4/${DATA}.${DATA_VERSION}.tar.gz http://geant4.cern.ch/support/source/${DATA}.${DATA_VERSION}.tar.gz; \
        tar zxf /opt/geant4/${DATA}.${DATA_VERSION}.tar.gz -C /opt/geant4/share/Geant4-${G4_VERSION}/data; \
    done && \
    rm -f /opt/geant4/*.tar.gz
