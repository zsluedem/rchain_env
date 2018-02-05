FROM ubuntu:16.04

RUN dpkg --add-architecture i386

RUN apt-get update && apt-get install -y python3-pip openjdk-8-jre-headless libstdc++6:i386 \
    cmake haskell-platform jflex apt-transport-https ca-certificates g++ g++-multilib openjdk-8-jre default-jdk
RUN pip3 install --upgrade pip
#

# install sbt
RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list &&\
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 &&\
    apt-get update && apt-get install -y sbt

# install bnfc
ADD dependencies /opt/
RUN cabal install --global /opt/bnfc/source

# install cup
RUN mkdir -p /root/.local/share/java/ && tar zxvf /opt/java-cup-bin-11b-20160615.tar.gz -C /root/.local/share/java/ \
        &&cp /opt/cup /bin/ && chmod a+x /bin/cup

CMD /bin/bash

