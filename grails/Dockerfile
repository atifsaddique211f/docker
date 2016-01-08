FROM phusion/baseimage:0.9.16
MAINTAINER Ahmad Iqbal <atif@aurorasolutions.io>

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Set customizable env vars defaults.
ENV GRAILS_VERSION 2.4.3
ENV JAVA_VER 7
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
ENV JAVA_OPTS -Xms256m -Xmx512m -XX:MaxPermSize=256m
ENV GRAILS_DEPENDENCY_CACHE_DIR /app/.m2/repository

RUN echo 'deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main' >> /etc/apt/sources.list && \
    echo 'deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main' >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C2518248EEA14886 && \
    apt-get update && \
    echo oracle-java${JAVA_VER}-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections && \
    apt-get install -y --force-yes --no-install-recommends oracle-java${JAVA_VER}-installer oracle-java${JAVA_VER}-set-default && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists && \
    rm -rf /var/cache/oracle-jdk${JAVA_VER}-installer

# Download Install utilities
RUN apt-get update
RUN apt-get install -y unzip wget
RUN apt-get install -y vim

# Install Grails
WORKDIR /usr/lib/jvm
RUN wget http://dist.springframework.org.s3.amazonaws.com/release/GRAILS/grails-$GRAILS_VERSION.zip
RUN unzip grails-$GRAILS_VERSION.zip
RUN rm -rf grails-$GRAILS_VERSION.zip
RUN ln -s grails-$GRAILS_VERSION grails

# Setup Grails path.
ENV GRAILS_HOME /usr/lib/jvm/grails
ENV PATH $GRAILS_HOME/bin:$PATH

# Clean up APT.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME ["/app"]
WORKDIR /app
