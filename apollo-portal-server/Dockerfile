# Dockerfile for apollo-portal-server

# Build with:
# docker build -t apollo-portal-server:v1.0.0 .

FROM openjdk:8-jre-alpine3.8
ENV VERSION 1.4.0
ENV URL https://github.com/ctripcorp/apollo/releases/download/v1.4.0/apollo-portal-1.4.0-github.zip
RUN \
    echo "http://mirrors.aliyun.com/alpine/v3.8/main" > /etc/apk/repositories && \
    echo "http://mirrors.aliyun.com/alpine/v3.8/community" >> /etc/apk/repositories  && \
    apk update upgrade && \
    apk add --no-cache procps curl bash tzdata && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    mkdir -p /apollo-portal-server

ADD . /apollo-portal-server/

RUN wget -O apollo-portal-${VERSION}-github.zip  $URL  \
    && unzip -n apollo-portal-${VERSION}-github.zip -d /apollo-portal-server \
    && mv /apollo-portal-server/apollo-portal-${VERSION}.jar /apollo-portal-server/apollo-portal.jar \
    && rm -rf apollo-portal-${VERSION}-github.zip \
    && rm -rf /apollo-portal-server/apollo-portal-${VERSION}-sources.jar


ENV APOLLO_PORTAL_SERVICE_NAME="service-apollo-portal-server.sre"

EXPOSE 8070

CMD ["/apollo-portal-server/scripts/startup-kubernetes.sh"]
