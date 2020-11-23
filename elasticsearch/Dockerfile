FROM elasticsearch:2.2

RUN \
  apt-get update -qq \
  && apt-get install -y vim \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD elasticsearch.yml /usr/share/elasticsearch/config/

RUN bin/plugin install royrusso/elasticsearch-hq/v2.0.3

