# Dockerfile for apollo-admin-server

# Build with:
# docker build -t apollo-admin-server:v1.0.0 .

FROM openjdk:8-jre-alpine3.8

RUN \
    echo "http://mirrors.aliyun.com/alpine/v3.8/main" > /etc/apk/repositories && \
    echo "http://mirrors.aliyun.com/alpine/v3.8/community" >> /etc/apk/repositories && \
    apk update upgrade && \
    apk add --no-cache procps curl bash tzdata && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    mkdir -p /apollo-admin-server

ADD . /apollo-admin-server/

ENV APOLLO_ADMIN_SERVICE_NAME="service-apollo-admin-server.sre"

ENV APOLLO_VERSION 1.7.1

RUN cd /apollo-admin-server && \
    wget https://github.com/ctripcorp/apollo/releases/download/v${APOLLO_VERSION}/apollo-adminservice-${APOLLO_VERSION}-github.zip && \
    unzip apollo-adminservice-1.7.1-github.zip "apollo-adminservice-${APOLLO_VERSION}.jar" && \
    rm -rf apollo-adminservice-${APOLLO_VERSION}-github.zip

EXPOSE 8090

CMD ["/apollo-admin-server/scripts/startup-kubernetes.sh"]
