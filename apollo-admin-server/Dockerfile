# Dockerfile for apollo-admin-server

# Build with:
# docker build -t apollo-admin-server:v1.0.0 .

FROM openjdk:8-jre-alpine3.8
ENV VERSION 1.4.0
ENV URL https://github.com/ctripcorp/apollo/releases/download/v1.4.0/apollo-adminservice-1.4.0-github.zip
RUN \
    echo "http://mirrors.aliyun.com/alpine/v3.8/main" > /etc/apk/repositories && \
    echo "http://mirrors.aliyun.com/alpine/v3.8/community" >> /etc/apk/repositories && \
    apk update upgrade && \
    apk add --no-cache procps curl bash tzdata && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    mkdir -p /apollo-admin-server

ADD . /apollo-admin-server/
RUN wget -O apollo-adminservice-${VERSION}-github.zip  $URL  \
    && unzip -n apollo-adminservice-${VERSION}-github.zip -d /apollo-admin-server \
    && mv /apollo-admin-server/apollo-adminservice-${VERSION}.jar /apollo-admin-server/apollo-adminservice.jar \
    && rm -rf apollo-adminservice-${VERSION}-github.zip \
    && rm -rf /apollo-admin-server/apollo-adminservice-${VERSION}-sources.jar

RUN chmod -R 755 /apollo-admin-server

ENV APOLLO_ADMIN_SERVICE_NAME="service-apollo-admin-server.sre"

EXPOSE 8090

CMD ["/apollo-admin-server/scripts/startup-kubernetes.sh"]
