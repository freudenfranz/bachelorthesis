FROM ubuntu:xenial

LABEL \
    description="Docker image containing the VSimRTI adapted OMNeT++ federate" \
    version="18.0" \
    maintainer="vsimrti@fokus.fraunhofer.de"

WORKDIR /home/vsimrti/bin/fed/omnetpp

COPY ./omnet* ./

RUN \
    apt-get update && \
    apt-get install -y --allow-unauthenticated \
    build-essential \
    bison \
    flex \
    libprotobuf-dev \
    protobuf-compiler \
    libxml2-dev \
    python \
    unzip \
    wget \
    zlib1g-dev && \
    ./omnet_installer.sh -p --simulator omnetpp-4.6-src.tgz --quiet

VOLUME ["/home/vsimrti/bin/fed/omnetpp/omnetpp-federate/configuration"]

EXPOSE 40001 40002

ENTRYPOINT \
    cp omnetpp-federate/configuration/omnetpp.ini omnetpp-federate/simulations/ && \
    omnetpp-federate/omnetpp-federate -u Cmdenv \
    -f omnetpp-federate/simulations/omnetpp.ini \
    -n 'omnetpp-federate;inet' \
    --vsimrtieventscheduler-host=0.0.0.0 \
    --vsimrtieventscheduler-port=40001 \
    --vsimrticmd-port=40002

