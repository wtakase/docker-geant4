Docker Geant4 images for ARM 32/64 bit machine
====

Docker image that Geant4 is installed.

This product includes software developed by Members of the Geant4 Collaboration ( http://cern.ch/geant4 ).

# Build the images on any CPU architecture machine
```
docker run --rm --privileged multiarch/qemu-user-static:register
git clone https://github.com/wtakase/docker-geant4
cd docker-geant4
git checkout release-10.5
docker build -f armhf-bionic/Dockerfile -t wtakase/geant4:10.05-armhf .
docker build -f arm64-bionic/Dockerfile -t wtakase/geant4:10.05-arm64 .
```

# Run on an ARM 32 bit machine
```
./download_dataset.sh /path/to/download/geant4/data  # Download dataset
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-armhf
```

# Run on an ARM 64 bit machine
```
./download_dataset.sh /path/to/download/geant4/data  # Download dataset
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-arm64
```

# Execute an example inside a container
```
apt-get update -y
apt-get install -y git
git clone https://github.com/Geant4/geant4.git
cd geant4
git checkout v10.5.0
cd examples/basic/B1
mkdir build
cd build
cmake ../
make
./exampleB1 run1.mac
```
