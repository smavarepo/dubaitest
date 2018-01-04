# Install packages
from ubuntu:16.04

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get -y install software-properties-common 

RUN  apt-get -y install python 
RUN  apt-get -y install iputils-ping 
RUN  apt-get -y install vim
RUN  apt-get -y install ssh 
RUN  apt-get -y  install net-tools
RUN  apt-get -y  install dnsutils
#add repositories needed
RUN add-apt-repository -y ppa:webupd8team/java 
RUN apt-get update 

# preaccept Oracle license
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections

#install java8 and ansible
RUN apt-get -y install oracle-java8-installer 

# Download and install jetty


RUN wget http://central.maven.org/maven2/org/eclipse/jetty/jetty-distribution/9.3.14.v20161028/jetty-distribution-9.3.14.v20161028.tar.gz && \
    tar -xzvf jetty-distribution-9.3.14.v20161028.tar.gz && \
    rm -rf jetty-distribution-9.3.14.v20161028.tar.gz && \
    mv jetty-distribution-9.3.14.v20161028 /opt/jetty

# Configure Jetty user and clean up install
RUN useradd jetty && \
    chown -R jetty:jetty /opt/jetty && \
    rm -rf /opt/jetty/webapps.demo
RUN cp /opt/jetty/bin/jetty.sh /etc/init.d/jetty

RUN chmod 777 /etc/init.d/jetty

RUN echo "JETTY_HOME=/opt/jetty" >> /etc/default/jetty
RUN echo "JETTY_USER=jetty" >> /etc/default/jetty
RUN echo "JETTY_PORT=8080" >> /etc/default/jetty
RUN echo "JETTY_LOGS=/opt/jetty/logs/" >> /etc/default/jetty
RUN echo "JETTY_BASE=/opt/jetty/" >> /etc/default/jetty
# Set defaults for docker run
WORKDIR /opt/jetty/
