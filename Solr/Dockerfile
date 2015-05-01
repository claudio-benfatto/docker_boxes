FROM foodityadmin/java7:0.1

MAINTAINER Claudio Benfatto

ENV SOLR_VERSION 0.0.4
ENV SOLR solr-$SOLR_VERSION

RUN export DEBIAN_FRONTEND=noninteractive && \
  apt-get update && \
  apt-get -y install lsof curl procps jsvc libcommons-daemon-java && \
  mkdir -p /opt && \
  wget -nv --output-document=/opt/$SOLR.deb \
  https://s3-eu-west-1.amazonaws.com/software.foodity.com/foodity-search-solr_0.0.4-SNAPSHOT_all.deb && \
  dpkg -i /opt/$SOLR.deb

  EXPOSE 8983
  CMD ["/bin/bash", "-c", "/etc/init.d/foodity-search-solr start; sleep 60; while curl --fail -X GET http://localhost:8983/solr/recipes/admin/ping?wt=json; do echo running; sleep 60; done"]
