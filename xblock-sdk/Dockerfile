FROM ubuntu:12.04
MAINTAINER stv <stv@stanford.edu>

# System Package Managment
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install apt-transport-https

# Source Control
RUN apt-get -y install git

# Build Tools
RUN apt-get -y install build-essential

# Python Development Packages
RUN apt-get -y install python
RUN apt-get -y install python-dev
RUN apt-get -y install python-distribute
RUN apt-get -y install python-pip

# These are needed to compile libxml
RUN apt-get -y install libxml2-dev
RUN apt-get -y install libxslt1-dev

# Grab source code
RUN git clone https://github.com/edx/xblock-sdk.git /xblock/sdk
RUN git clone https://github.com/Stanford-Online/xblock-factory.git /xblock/factory

# Build source code
WORKDIR /xblock/sdk
RUN pip install setuptools>=17.1 --upgrade
RUN pip install funcsigs
RUN make install

# Install node/npm
RUN apt-get install -y python-software-properties
RUN add-apt-repository ppa:chris-lea/node.js
RUN apt-get -y update
RUN apt-get -y install nodejs

# Run websever
ENV HOME /xblock/sdk
EXPOSE 8002
CMD ["/usr/bin/python", "./manage.py", "runserver", "0:8002"]
