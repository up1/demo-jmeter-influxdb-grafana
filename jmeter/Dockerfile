FROM alpine:3.15

ARG JMETER_VERSION="5.6.2"

ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV JMETER_BIN  ${JMETER_HOME}/bin
ENV MIRROR_HOST http://mirrors.ocf.berkeley.edu/apache/jmeter
ENV JMETER_DOWNLOAD_URL ${MIRROR_HOST}/binaries/apache-jmeter-${JMETER_VERSION}.tgz
ENV JMETER_PLUGINS_FOLDER ${JMETER_HOME}/lib/ext/

RUN apk update \
	&& apk upgrade \
	&& apk add ca-certificates \
	&& update-ca-certificates \
            && apk add --update openjdk17-jre tzdata curl unzip bash \
            # && cp /usr/share/zoneinfo/Asia/Bangkok /etc/localtime \
            # && echo "Asia/Bangkok" >  /etc/timezone \
	&& rm -rf /var/cache/apk/* \
	&& mkdir -p /tmp/dependencies  \
	&& curl -L --silent ${JMETER_DOWNLOAD_URL} >  /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz  \
	&& mkdir -p /opt  \
	&& tar -xzf /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz -C /opt  \
	&& rm -rf /tmp/dependencies


ENV PATH $PATH:$JMETER_BIN

COPY jmeter-plugins-influxdb2-listener-2.6.jar ${JMETER_PLUGINS_FOLDER}/jmeter-plugins-influxdb2-listener-2.6.jar
RUN mkdir /app
RUN chmod -R a+w  /app
COPY launch.sh /app/launch.sh
RUN chmod a+x /app/launch.sh
COPY google.jmx /app/google.jmx


WORKDIR ${JMETER_HOME}

ENTRYPOINT ["/app/launch.sh"]