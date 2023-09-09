FROM patilarpith/stretch-utils as downloader
ENV GOVERSION 1.20.2
RUN mkdir /usr/local/go
RUN mkdir /root/.go
RUN wget -qO- https://golang.org/dl/go${GOVERSION}.linux-amd64.tar.gz | \
  tar -C /usr/local/go --strip-components=1 -xzf -

RUN mkdir -p /app
WORKDIR /app
ENV GOROOT='/usr/local/go'
ENV GOPATH='/root/.go'
ENV PATH=$PATH:$GOROOT/bin
RUN GO111MODULE=on go install golang.org/x/tools/gopls@v0.13.2
RUN rm -r /usr/local/go/doc
ENV PATH=$PATH:$GOROOT/bin

ENV LANGUAGE='go'
