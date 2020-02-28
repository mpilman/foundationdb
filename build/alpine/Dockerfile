FROM alpine:3.10
LABEL version=1.0.0
ENV DOCKER_IMAGEVER=1.0.0

RUN echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && apk update
RUN apk add clang mono@testing ccache distcc make cmake \
            openjdk11 py-pip python3 ruby go npm libressl-dev \
            curl

USER root

RUN adduser -D fdb && chown fdb /opt

# wget of bintray without forcing UTF-8 encoding results in 403 Forbidden
RUN cd /opt/ &&\
    curl -L https://dl.bintray.com/boostorg/release/1.71.0/source/boost_1_71_0.tar.bz2 > boost_1_71_0.tar.bz2 &&\
		echo "d73a8da01e8bf8c7eda40b4c84915071a8c8a0df4a6734537ddde4a8580524ee  boost_1_71_0.tar.bz2" > boost-sha.txt &&\
		sha256sum -c boost-sha.txt &&\
    tar -xjf boost_1_71_0.tar.bz2 &&\
    rm -rf boost_1_71_0.tar.bz2 boost-sha.txt boost_1_71_0/libs

RUN apk add bash git g++ gcc m4 linux-headers

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk
ENV PATH="${JAVA_HOME}/bin:$PATH"
ENV CC=/usr/bin/gcc
ENV CXX=/usr/bin/g++
ENV TLS_LIBDIR=/usr/lib/
