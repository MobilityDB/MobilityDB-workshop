ARG POSTGRES_VERSION
ARG POSTGIS_VERSION

FROM postgis/postgis:$POSTGRES_VERSION-$POSTGIS_VERSION

# Configuration Parameters
LABEL maintainer="MobilityDB Project - https://github.com/MobilityDB/MobilityDB"
ENV POSTGRES_DB=mobilitydb
ENV POSTGRES_USER=docker
ENV POSTGRES_PASSWORD=docker
ENV MOBILITYDB_VERSION $MOBDB_VERSION

# Fix the Release file expired problem
RUN echo "Acquire::Check-Valid-Until \"false\";\nAcquire::Check-Date \"false\";" | cat > /etc/apt/apt.conf.d/10no--check-valid-until


# Install Prerequisites
RUN apt-get update \
 && apt-get install -y \
    build-essential \
    cmake \
    git \
    libproj-dev \
    g++ \
    wget \
    unzip \
    autoconf \
    autotools-dev \
    libgeos-dev \
    libpq-dev \
    libproj-dev \
    libjson-c-dev \
    protobuf-c-compiler \
    xsltproc \
    libgsl-dev \
    libgslcblas0 \
    postgresql-server-dev-${PG_MAJOR} \
  && rm -rf /var/lib/apt/lists/*

# Install MobilityDB
RUN git clone https://github.com/MobilityDB/MobilityDB.git -b develop /usr/local/src/MobilityDB && \
    mkdir -p /usr/local/src/MobilityDB/build && \
    cd /usr/local/src/MobilityDB/build && \
    cmake .. && \
    make -j$(nproc) && \
    make install

# Workshop Data
RUN mkdir /Workshop
RUN cd /Workshop && \
    wget https://raw.githubusercontent.com/MobilityDB/MobilityDB-workshop/master/data/gtfs_data.zip && \
    wget https://raw.githubusercontent.com/MobilityDB/MobilityDB-workshop/master/data/ais_data.zip && \
    unzip gtfs_data.zip -d gtfs_data && \
    unzip ais_data.zip -d ais_data && \   
    rm -f ais_data.zip gtfs_data.zip

RUN rm /docker-entrypoint-initdb.d/10_postgis.sh
COPY ./docker/initdb-mobilitydb.sh /docker-entrypoint-initdb.d/mobilitydb.sh
RUN chmod +x /docker-entrypoint-initdb.d/mobilitydb.sh
RUN chmod a+r /Workshop/*
