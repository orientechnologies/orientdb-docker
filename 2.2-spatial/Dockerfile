############################################################
# Dockerfile  for OrientDB with spatial module
############################################################

FROM orientdb:2.2.3

ENV ORIENTDB_DOWNLOAD_SPATIAL_MD5 6c2209f137a6363e60c88fd0412c35ac
ENV ORIENTDB_DOWNLOAD_SPATIAL_SHA1 ce4f8541e8994a7edaae05af96b3b36a8a1bd537

ENV ORIENTDB_DOWNLOAD_SPATIAL_URL ${ORIENTDB_DOWNLOAD_SERVER:-http://central.maven.org/maven2/com/orientechnologies}/orientdb-spatial/$ORIENTDB_VERSION/orientdb-spatial-$ORIENTDB_VERSION-dist.jar

RUN wget $ORIENTDB_DOWNLOAD_SPATIAL_URL \
    && echo "$ORIENTDB_DOWNLOAD_SPATIAL_MD5 *orientdb-spatial-$ORIENTDB_VERSION-dist.jar" | md5sum -c - \
    && echo "$ORIENTDB_DOWNLOAD_SPATIAL_SHA1 *orientdb-spatial-$ORIENTDB_VERSION-dist.jar" | sha1sum -c - \
    && mv orientdb-spatial-*-dist.jar /orientdb/lib/

