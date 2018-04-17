############################################################
# Dockerfile to run an OrientDB (Graph) Container
############################################################

FROM openjdk:8-jdk-alpine

MAINTAINER OrientDB LTD (info@orientdb.com)

# Override the orientdb download location with e.g.:
#   docker build -t mine --build-arg ORIENTDB_DOWNLOAD_SERVER=http://repo1.maven.org/maven2/com/orientechnologies/ .
ARG ORIENTDB_DOWNLOAD_SERVER

ENV ORIENTDB_VERSION 3.0.0
ENV ORIENTDB_DOWNLOAD_LOCATION ${ORIENTDB_DOWNLOAD_SERVER:-http://central.maven.org/maven2/com/orientechnologies}/orientdb-community/$ORIENTDB_VERSION
ENV ORIENTDB_DOWNLOAD_NAME orientdb-community-$ORIENTDB_VERSION
ENV ORIENTDB_DOWNLOAD_MD5 $ORIENTDB_DOWNLOAD_LOCATION/$ORIENTDB_DOWNLOAD_NAME.tar.gz.md5
ENV ORIENTDB_DOWNLOAD_SHA1 $ORIENTDB_DOWNLOAD_LOCATION/$ORIENTDB_DOWNLOAD_NAME.tar.gz.sha1
ENV ORIENTDB_DOWNLOAD_URL $ORIENTDB_DOWNLOAD_LOCATION/$ORIENTDB_DOWNLOAD_NAME.tar.gz

RUN apk add --update tar curl \
    && rm -rf /var/cache/apk/*

#download distribution tar, untar and delete databases
RUN mkdir /orientdb && \
  wget $ORIENTDB_DOWNLOAD_URL \
  && wget $ORIENTDB_DOWNLOAD_MD5 \
  && wget $ORIENTDB_DOWNLOAD_SHA1 \
  && sed -i 's/$/ '*$ORIENTDB_DOWNLOAD_NAME'.tar.gz/' $ORIENTDB_DOWNLOAD_NAME.tar.gz.md5 \
  && cat $ORIENTDB_DOWNLOAD_NAME.tar.gz.md5 | md5sum -c - \
  && sed -i 's/$/ '*$ORIENTDB_DOWNLOAD_NAME'.tar.gz/' $ORIENTDB_DOWNLOAD_NAME.tar.gz.sha1 \
  && cat $ORIENTDB_DOWNLOAD_NAME.tar.gz.sha1 | sha1sum -c - \
  && tar -xvzf orientdb-community-$ORIENTDB_VERSION.tar.gz -C /orientdb --strip-components=1 \
  && rm $ORIENTDB_DOWNLOAD_NAME.tar.gz \
  && rm -f $ORIENTDB_DOWNLOAD_NAME.tar.gz.* \
  && rm -rf /orientdb/databases/*


ENV PATH /orientdb/bin:$PATH

VOLUME ["/orientdb/backup", "/orientdb/databases", "/orientdb/config"]

WORKDIR /orientdb

#OrientDb binary
EXPOSE 2424

#OrientDb http
EXPOSE 2480

# Default command start the server
CMD ["server.sh"]

