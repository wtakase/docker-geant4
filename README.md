Ubuntu/Alpine Linux based Docker Geant4 images for AMD64
====

Docker image that Geant4 is installed.

This product includes software developed by Members of the Geant4 Collaboration ( http://cern.ch/geant4 ).

## Download Geant4 dataset to your Docker host
```
git clone --branch v10.5.0-qt https://github.com/wtakase/docker-geant4
./docker-geant4/download_dataset.sh /path/to/download/geant4/data
```

## Launch a container

### on AMD64 Docker host

#### Ubuntu 18.04 LTS (Bionic Beaver)

```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-qt-amd64-bionic
```

#### Alpine Linux 3.9

```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" wtakase/geant4:10.05-qt-amd64-alpine
```

## Execute a Geant4 example
```
git clone --branch v10.5.0 https://github.com/Geant4/geant4.git
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" -v "`pwd`/geant4/examples:/opt/geant4/examples:ro" wtakase/geant4:10.05-qt-amd64-bionic bash -c 'cmake /opt/geant4/examples/basic/B1 && make && ./exampleB1 run1.mac'
```

### Qt visualization
```
docker run --rm -it -v "/path/to/download/geant4/data:/opt/geant4/data:ro" -v "`pwd`/geant4/examples:/opt/geant4/examples:ro" --net host -e DISPLAY=$DISPLAY -v $HOME/.Xauthority:/root/.Xauthority wtakase/geant4:10.05-qt-amd64-bionic bash -c 'cmake /opt/geant4/examples/basic/B1 && make && ./exampleB1'
```

## Build images
```
git clone --branch v10.5.0-qt https://github.com/wtakase/docker-geant4
cd docker-geant4
docker build -f amd64/bionic/Dockerfile -t wtakase/geant4:10.05-qt-amd64-bionic .
docker build -f amd64/alpine/Dockerfile -t wtakase/geant4:10.05-qt-amd64-alpine .
```
