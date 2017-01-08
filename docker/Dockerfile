FROM buildpack-deps:jessie-curl

VOLUME /mnt/routes
EXPOSE 80

ARG version=origin/master
RUN set -x && \
    apt-get update -y && apt-get -y install apt-utils && \
    apt-get -y install git ca-certificates wget file gcc && \
    mkdir /go && mkdir /golang && cd /golang && \
    wget https://storage.googleapis.com/golang/go1.7.4.linux-amd64.tar.gz && \
    tar xzvf go1.7.4.linux-amd64.tar.gz && \
    export GOROOT=/golang/go && \
    export PATH=$GOROOT/bin:$PATH && \
    export GOPATH=/go && \
    go version && \
    go get -t -d -v  github.com/gliderlabs/logspout && \
    cd /go/src/github.com/gliderlabs/logspout/ && \
    git reset --hard ${version} && \
    echo Logspout working copy at $(git describe --always) && \
    go get -v -d -t github.com/ezh/logspout-logstash && \
    cp -r /go/src/github.com/ezh/logspout-logstash/ /go/src/github.com/gliderlabs/logspout/adapters/logstash/ && \
    go get -v -d -t github.com/ezh/logspout-kafka && \
    cp -r /go/src/github.com/ezh/logspout-kafka/ /go/src/github.com/gliderlabs/logspout/adapters/kafka/ && \
    go get -v -d -t github.com/ezh/logspout-redis-logstash && \
    cp -r /go/src/github.com/ezh/logspout-redis-logstash/ /go/src/github.com/gliderlabs/logspout/adapters/redis/ && \
    go get -v -d -t github.com/ezh/logspout-beat && \
    cp -r /go/src/github.com/ezh/logspout-beat/ /go/src/github.com/gliderlabs/logspout/adapters/beat/ && \
    go get -v -d -t github.com/ezh/logspout-splunk && \
    cp -r /go/src/github.com/ezh/logspout-splunk/ /go/src/github.com/gliderlabs/logspout/adapters/splunk/ && \
    go get -v -d -t github.com/ezh/logspout-fluentd && \
    cp -r /go/src/github.com/ezh/logspout-fluentd/ /go/src/github.com/gliderlabs/logspout/adapters/fluentd/ && \
    go get -v -d -t github.com/ezh/logspout-kinesis && \
    cp -r /go/src/github.com/ezh/logspout-kinesis/ /go/src/github.com/gliderlabs/logspout/adapters/kinesis/ && \
    go get -v -d -t github.com/ezh/logspout-gelf && \
    cp -r /go/src/github.com/ezh/logspout-gelf/ /go/src/github.com/gliderlabs/logspout/adapters/gelf/ && \
    go get -v -d -t github.com/ezh/logspout-cloudwatch && \
    cp -r /go/src/github.com/ezh/logspout-cloudwatch/ /go/src/github.com/gliderlabs/logspout/adapters/cloudwatch/ && \
    rm -rf /go/src/github.com/gliderlabs/logspout/adapters/cloudwatch/docker/ && \
    go get -v -d -t github.com/ezh/logspout-logentries-autowire && \
    cp -r /go/src/github.com/ezh/logspout-logentries-autowire/ /go/src/github.com/gliderlabs/logspout/adapters/logentries/ && \
    echo 'package main\n\
\n\
import (\n\
        _ "github.com/gliderlabs/logspout/adapters/beat"\n\
        _ "github.com/gliderlabs/logspout/adapters/cloudwatch"\n\
        _ "github.com/gliderlabs/logspout/adapters/fluentd"\n\
        _ "github.com/gliderlabs/logspout/adapters/gelf"\n\
        _ "github.com/gliderlabs/logspout/adapters/kafka"\n\
        _ "github.com/gliderlabs/logspout/adapters/kinesis"\n\
        _ "github.com/gliderlabs/logspout/adapters/logentries"\n\
        _ "github.com/gliderlabs/logspout/adapters/logstash"\n\
        _ "github.com/gliderlabs/logspout/adapters/raw"\n\
        _ "github.com/gliderlabs/logspout/adapters/redis"\n\
        _ "github.com/gliderlabs/logspout/adapters/splunk"\n\
        _ "github.com/gliderlabs/logspout/adapters/syslog"\n\
        _ "github.com/gliderlabs/logspout/httpstream"\n\
        _ "github.com/gliderlabs/logspout/routesapi"\n\
        _ "github.com/gliderlabs/logspout/transports/tcp"\n\
        _ "github.com/gliderlabs/logspout/transports/udp"\n\
        _ "github.com/gliderlabs/logspout/transports/tls"\n\
)\n' > modules.go && \
    go get -t ./adapters/... && \
    go test ./adapters/... && \
    go build && \
    cp logspout /usr/bin && \
    rm -rf /go && \
    rm -rf /golang && \
    apt-get clean && \
    rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/* /download/directory

COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

CMD ["logspout"]
