#
# Follow platform guideline specified in https://github.com/docker-library/official-images
# Reference:
#  - https://mosquitto.org/2013/01/mosquitto-debian-repository/
#

FROM arm32v7/debian:jessie
MAINTAINER Somsak Chartsrisak <somsakc@mbixtech.com>

LABEL description="Eclipse Mosquitto MQTT Broker"
LABEL vendor="MBIX TECH"
LABEL version="1.1"

RUN apt-get update && \
    apt-get -y install wget

RUN wget http://repo.mosquitto.org/debian/mosquitto-repo.gpg.key && \
    apt-key add mosquitto-repo.gpg.key && \
    rm -f mosquitto-repo.gpg.key && \
    cd /etc/apt/sources.list.d/ && \
    wget http://repo.mosquitto.org/debian/mosquitto-jessie.list && \
    apt-get update && \
    apt-get -y install mosquitto

RUN mkdir -p /mosquitto/config /mosquitto/data /mosquitto/log && \
    chown -R mosquitto:mosquitto /mosquitto

COPY config/mosquitto.conf /mosquitto/config

COPY docker-entrypoint.sh /

RUN chown mosquitto:mosquitto /docker-entrypoint.sh && \
    chmod ug+x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["/usr/sbin/mosquitto", "-c", "/mosquitto/config/mosquitto.conf"]

