# skywakling-jdk-dockerimage

- 2020/1/8 -> jdk8u232

`[root@vm1 skywalking]# pwd`<br />
/skywalking<br />
`[root@vm1 skywalking]# tree`<br />
├── config<br />
│   └── agent.config<br />
├── Dockerfile<br />
└── skywalking-agent.jar<br />

1 directory, 3 files




//anapsix/alpine-java:8_server-jre_unlimited<br/>
//RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

<br />
<br />
<br />

- 2021/5/18 -> jdk8u282 & *新增字体包*

```
FROM adoptopenjdk/openjdk8-openj9:jdk8u282-b08_openj9-0.24.0-alpine-slim

ENV LANG C.UTF-8

#utc+8 china
RUN apk add -U tzdata && rm -rf /etc/localtime && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' > /etc/timezone

#font package
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN set -xe && apk --no-cache add ttf-dejavu fontconfig

#skywalking agent
ADD skywalking-agent.jar /skywalking/skywalking-agent.jar
ADD config/agent.config /skywalking/config/agent.config

```
