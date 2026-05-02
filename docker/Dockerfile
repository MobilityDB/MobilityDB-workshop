ARG POSTGRES_VERSION=18
ARG POSTGIS_VERSION=3.6
ARG MOBILITYDB_VERSION=1.3

FROM mobilitydb/mobilitydb:${POSTGRES_VERSION}-${POSTGIS_VERSION}-${MOBILITYDB_VERSION}

LABEL maintainer="MobilityDB Project - https://github.com/MobilityDB/MobilityDB"

ENV POSTGRES_DB=mobilitydb
ENV POSTGRES_USER=docker
ENV POSTGRES_PASSWORD=docker

RUN apt-get update \
    && apt-get install -y --no-install-recommends unzip \
    && rm -rf /var/lib/apt/lists/*

COPY ./data/gtfs_data.zip ./data/ais_data.zip /tmp/
RUN mkdir /Workshop \
    && cd /Workshop \
    && unzip -o /tmp/gtfs_data.zip -d gtfs_data \
    && unzip -o /tmp/ais_data.zip -d ais_data \
    && rm /tmp/gtfs_data.zip /tmp/ais_data.zip \
    && chmod -R a+r /Workshop
