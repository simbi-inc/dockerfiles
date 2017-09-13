FROM simbi/app:latest

RUN \
  wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - \
    | apt-key add - \
    && sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

RUN \
  apt-get -qq update \
    && apt-get install --only-upgrade openssl \
    && apt-get install -y \
      less \
      libpq5 \
      locales \
      postgresql-client-9.5 \
      silversearcher-ag \
      shellcheck \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN locale-gen C.UTF-8 || true
ENV LANG=C.UTF-8

RUN \
  PHANTOMJS_URL="https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/phantomjs-latest.tar.bz2" \
    && apt-get install libfontconfig \
    && curl --silent --show-error --location --fail --retry 3 --output /tmp/phantomjs.tar.bz2 ${PHANTOMJS_URL} \
    && tar -x -C /tmp -f /tmp/phantomjs.tar.bz2 \
    && mv /tmp/phantomjs-*-linux-x86_64/bin/phantomjs /usr/local/bin \
    && rm -rf /tmp/phantomjs.tar.bz2 /tmp/phantomjs-* \
    && phantomjs --version

ENV DISPLAY :99
RUN \
  printf '#!/bin/sh\nXvfb :99 -screen 0 1280x1024x24 &\nexec "$@"\n' > /tmp/entrypoint \
    && chmod +x /tmp/entrypoint \
    && mv /tmp/entrypoint /docker-entrypoint.sh

LABEL com.circleci.preserve-entrypoint=true

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/sh"]
