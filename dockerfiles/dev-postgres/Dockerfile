FROM postgres

RUN apt-get update -y && apt-get install -y --no-install-recommends \
  ca-certificates \
  curl \
  dnsutils \
  git \
  jq \
  iptables \
  g++ \
  netcat \
  kmod \
  &&  apt-get autoremove -yqq \
  &&  apt-get clean \
  &&  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl -L "https://packages.cloudfoundry.org/stable?release=linux64-binary&version=6.43.0&source=github-rel" | tar -zx && mv cf /usr/local/bin/cf

ADD go*.tar.gz /usr/local

ENV GOPATH /gopath
ENV GOBIN /gopath/bin
ENV PATH $PATH:/usr/local/go/bin:$GOPATH/bin

RUN go get github.com/tools/godep
RUN go get github.com/onsi/ginkgo

RUN go install github.com/onsi/ginkgo/ginkgo

CMD /bin/bash
