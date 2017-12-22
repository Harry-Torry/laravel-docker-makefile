FROM centos:latest

MAINTAINER david@codesmith.tech

RUN yum install -y telnet

RUN curl -o node-v8.9.1-linux-x64.xz https://nodejs.org/dist/v8.9.1/node-v8.9.1-linux-x64.tar.xz && \
    tar -xv --xz -f node-v8.9.1-linux-x64.xz && \
    cd node-v8.9.1-linux-x64 && \
    cp -R bin /usr/local && \
    cp -R include /usr/local && \
    cp -R lib /usr/local && \
    cp -R share /usr/local && \
    cd .. && \
    rm -rf node-*

RUN npm install  --unsafe -g laravel-echo-server

WORKDIR /app