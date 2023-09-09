ARG VERSION=3.2.2

FROM ruby:3.2.2 as downloader

RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/ruby-${VERSION}-0-linux-amd64-debian-10.tar.gz && \
    echo "40ce137a4ddb3e6e5a77eeb6d40c960478b9fc665b6510701a5f00a36acbed5c  /tmp/bitnami/pkg/cache/ruby-${VERSION}-0-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/ruby-${VERSION}-0-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/ruby-${VERSION}-0-linux-amd64-debian-10.tar.gz

FROM ruby:3.2.2
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libreadline-dev \
    libyaml-dev \
    libffi-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-0-2 \
    rubygems \
    curl \
    gnupg2 \
    ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN update-ca-certificates

RUN apt-get update && \
    apt-get install -y --no-install-recommends ruby-all-dev

RUN gem install --no-document nokogiri --pre
RUN gem sources --add https://rubygems.org/ && gem clean
RUN gem install --no-document solargraph -v 0.49.0 && \
    solargraph clear-cores && \
    solargraph download-core

ENV LANGUAGE='ruby'
