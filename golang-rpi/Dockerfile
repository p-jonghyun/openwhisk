
FROM arm32v7/golang:1.11

RUN echo "deb http://deb.debian.org/debian stretch-backports main contrib non-free" >>/etc/apt/sources.list \
    && apt-get update \
    && apt-get -y --no-install-recommends upgrade \
    && apt-get -y --no-install-recommends install \
                        curl jq git \
                        librdkafka1=0.11.6-1~bpo9+1 \
                        librdkafka++1=0.11.6-1~bpo9+1 \
                        librdkafka-dev=0.11.6-1~bpo9+1 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir /action

WORKDIR /action
ADD proxy /bin/proxy
ADD gobuild.py /bin/compile
ADD gobuild.py.launcher.go /bin/compile.launcher.go
ENV OW_COMPILER=/bin/compile
ENTRYPOINT [ "/bin/proxy" ]
