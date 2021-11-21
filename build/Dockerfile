FROM ubuntu:18.04

RUN echo "alias ll='ls -l'" >> /root/.bashrc
RUN apt-get update
RUN apt-get install -q -y git subversion build-essential gawk unzip libncurses5-dev zlib1g-dev python libssl-dev
RUN apt-get install -q -y gcc g++ wget
RUN echo "export FORCE_UNSAFE_CONFIGURE=1" >> /root/.bashrc
COPY . /etc/gluon