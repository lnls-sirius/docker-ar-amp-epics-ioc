Docker image to run the AR Amplifier EPICS IOC
==================================================================

This repository contains the Dockerfile used to create the Docker image to run the
[AR Amplifier EPICS IOC](https://github.com/lnls-dig/ar-amp-epics-ioc).

## Running the IOC

The simples way to run the IOC is to run:

    docker run --rm -it --net host lnlsdig/ar-amp-epics-ioc -i IPADDR -p PORT -P PREFIX1 -R PREFIX2

where `IPADDR` and `PORT` are the IP address and port of the device
to connect to, and `PREFIX1` and `PREFIX2` are the prefixes to be
added before the PV name.
The options you can specify (after `lnlsdig/ar-amp-epics-ioc`) are:

- `-i IPADDR`: device IP address to connect to (required)
- `-p PORT`: device port number to connect to (required)
- `-P PREFIX1`: the value of the EPICS `$(P)` macro used to prefix the PV names
- `-R PREFIX2`: the value of the EPICS `$(R)` macro used to prefix the PV names
- `-t TELNET_PORT`: the telnet port used to access the IOC shell

## Creating a Persistent Container

If you want to create a persistent container to run the IOC, you can run a
command similar to:

    docker run -it --net host --restart always --name CONTAINER_NAME lnlsdig/ar-amp-epics-ioc -i IPADDR -p PORT -P PREFIX1 -R PREFIX2

where `IPADDR`, `PORT`, `PREFIX1`, and `PREFIX2` are as in the previous
section and `CONTAINER_NAME` is the name given to the container. You can also use
the same options as described in the previous section.

## Building the Image Manually

To build the image locally without downloading it from Docker Hub, clone the
repository and run the `docker build` command:

    git clone https://github.com/lnls-dig/docker-ar-amp-epics-ioc
    docker build -t lnlsdig/ar-amp-epics-ioc docker-ar-amp-epics-ioc
