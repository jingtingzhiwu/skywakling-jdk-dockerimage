# 注意Linux 宿主机的时区 = Docker容器时区(skywalking oap server/skywalking ui/es) = agent客户端时区 

- 2020/1/8 -> jdk8u232

`[root@vm1 skywalking]# pwd`<br />
/skywalking<br />
`[root@vm1 skywalking]# tree`<br />
├── config<br />
│   └── agent.config<br />
├── Dockerfile<br />
└── skywalking-agent.jar<br />
└── ...        <br />

6 directory, 105 files




//anapsix/alpine-java:8_server-jre_unlimited<br/>
//RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

<br />
<br />
<br />

- 2021/5/18 -> jdk8u282 & *新增字体包*

```
FROM adoptopenjdk/openjdk8-openj9:jdk8u282-b08_openj9-0.24.0-alpine-slim

MAINTAINER admin@wilkey.vip

ENV LANG C.UTF-8

#utc+8 china
RUN apk add -U tzdata && rm -rf /etc/localtime && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' > /etc/timezone

#font package
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN set -xe && apk --no-cache add ttf-dejavu fontconfig

#skywalking agent
ADD skywalking-agent.jar /skywalking/skywalking-agent.jar
ADD config/agent.config /skywalking/config/agent.config
COPY activations /skywalking/activations
COPY bootstrap-plugins /skywalking/bootstrap-plugins
COPY optional-plugins /skywalking/optional-plugins
COPY optional-reporter-plugins /skywalking/optional-reporter-plugins
COPY plugins /skywalking/plugins

```
