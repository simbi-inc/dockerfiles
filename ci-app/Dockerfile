FROM simbi/app:latest

RUN \
  wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - \
  | apt-key add - \
  && sh -c 'echo "deb https://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

RUN \
  apt-get -qq update \
  && apt-get install --only-upgrade openssl \
  && apt-get install -y \
  libpq5 \
  postgresql-client-9.6 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV CHROME_VERSION=99.0.4844.51-1

# setup chrome for system specs
RUN curl -sS -L https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list \
  && apt-get update -qq \
  && apt-get install --no-install-recommends -yqq google-chrome-stable \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/sh"]
