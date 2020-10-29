############################################################
# Dockerfile to run an OrientDB (Graph) Container
############################################################

FROM registry.access.redhat.com/rhel7

MAINTAINER OrientDB LTD (info@orientdb.com)

# Override the orientdb download location with e.g.:
#   docker build -t mine --build-arg ORIENTDB_DOWNLOAD_SERVER=https://repo1.maven.org/maven2/com/orientechnologies/ .
ARG ORIENTDB_DOWNLOAD_SERVER

ENV ORIENTDB_VERSION 2.2.37
ENV ORIENTDB_DOWNLOAD_MD5 cb80556ef3b0260d0ee5de88ea73fb9d
ENV ORIENTDB_DOWNLOAD_SHA1 469c402dde029f265fe905de2c08b43960e81f07

ENV ORIENTDB_DOWNLOAD_URL ${ORIENTDB_DOWNLOAD_SERVER:-https://repo1.maven.org/maven2/com/orientechnologies}/orientdb-community/$ORIENTDB_VERSION/orientdb-community-$ORIENTDB_VERSION.tar.gz

LABEL name="orientdb/orientdb" \
      vendor="OrientDB LTD." \
      version="2.2" \
      release=“37” \
      summary="OrientDB multi-model database" \
      description="OrientDB multi-model database" \
### Recommended labels below
      url="https://www.orientdb.com" \
      run='docker run -tdi --name ${NAME} ${IMAGE}' \
      io.k8s.description="OrientDB multi-model database" \
      io.k8s.display-name="OrientDB multi-model database" \
      io.openshift.expose-services="" \
      io.openshift.tags="orientdb"

#Install JDK and necessary applications
RUN yum -y install --disablerepo "*" --enablerepo rhel-7-server-rpms --setopt=tsflags=nodocs \
      java-1.8.0-openjdk wget && \
    yum clean all

#download distribution tar, untar and delete databases
RUN mkdir /orientdb && \
    wget  $ORIENTDB_DOWNLOAD_URL && \
    echo "$ORIENTDB_DOWNLOAD_MD5 *orientdb-community-$ORIENTDB_VERSION.tar.gz" | md5sum -c - && \
    echo "$ORIENTDB_DOWNLOAD_SHA1 *orientdb-community-$ORIENTDB_VERSION.tar.gz" | sha1sum -c -&& \
    tar -xvzf orientdb-community-$ORIENTDB_VERSION.tar.gz -C /orientdb --strip-components=1 && \
    mkdir /licenses && \
    cp /orientdb/license.txt /licenses/ && \
    rm orientdb-community-$ORIENTDB_VERSION.tar.gz && \
    rm -rf /orientdb/databases/* && \
    chown -R 99 /orientdb && \
    chmod -R g=u /orientdb

ADD help.1 /help.1

ENV PATH /orientdb/bin:$PATH

VOLUME ["/orientdb/backup", "/orientdb/databases", "/orientdb/config"]

WORKDIR /orientdb

#OrientDb binary
EXPOSE 2424

#OrientDb http
EXPOSE 2480

#Switch to non-root user
USER 99

#Default command start the server
CMD ["server.sh"]
