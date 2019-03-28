Ubuntu/Alpine Linux based Docker Geant4 images for AMD64, ARM32, ARM64
====

Docker image that Geant4 is installed.

This product includes software developed by Members of the Geant4 Collaboration ( http://cern.ch/geant4 ).

## Download Geant4 dataset to your Docker host
```
git clone --branch v10.5.0 https://github.com/wtakase/docker-geant4
./docker-geant4/download_dataset.sh /path/to/download/geant4/data
```

## Launch a container

### on AMD64 Docker host

#### Ubuntu 18.04 LTS (Bionic Beaver)

```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-amd64-bionic
```

#### Alpine Linux 3.9

```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-amd64-alpine
```

### on ARM32 Docker host

#### Ubuntu 18.04 LTS (Bionic Beaver)

```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-armhf-bionic
```

#### Alpine Linux 3.9

```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-armhf-alpine
```

### on ARM64 Docker host

#### Ubuntu 18.04 LTS (Bionic Beaver)

```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-arm64-bionic
```

#### Alpine Linux 3.9

```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-arm64-alpine
```

## Execute a Geant4 example
```
git clone --branch v10.5.0 https://github.com/Geant4/geant4.git
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" -v "`pwd`/geant4/examples:/opt/geant4/examples:ro" wtakase/geant4:10.05-amd64-bionic bash -c 'cmake /opt/geant4/examples/basic/B1 && make && ./exampleB1 run1.mac'
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" -v "`pwd`/geant4/examples:/opt/geant4/examples:ro" -v "/tmp/output:/tmp/output" wtakase/geant4:10.05-amd64-bionic bash -c 'cmake /opt/geant4/examples/extended/medical/electronScattering2 && make && sed -i "\/run\/initialize/i /run/numberOfThreads 8" macros/Opt0/Al1_13MeV.mac && ./electronScattering2 macros/Opt0/Al1_13MeV.mac 1 /tmp/output/Opt0_Al1_13MeV_1.csv'
```

## Build images on any CPU architecture machine
```
docker run --rm --privileged multiarch/qemu-user-static:register
git clone --branch v10.5.0 https://github.com/wtakase/docker-geant4
cd docker-geant4
docker build -f amd64/bionic/Dockerfile -t wtakase/geant4:10.05-amd64-bionic .
docker build -f amd64/alpine/Dockerfile -t wtakase/geant4:10.05-amd64-alpine .
docker build -f armhf/bionic/Dockerfile -t wtakase/geant4:10.05-armhf-bionic .
docker build -f armhf/alpine/Dockerfile -t wtakase/geant4:10.05-armhf-alpine .
docker build -f arm64/bionic/Dockerfile -t wtakase/geant4:10.05-arm64-bionic .
docker build -f arm64/alpine/Dockerfile -t wtakase/geant4:10.05-arm64-alpine .
```
