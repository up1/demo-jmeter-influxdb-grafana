FROM alpine/jmeter:5.6
ENV JMETER_PLUGINS_FOLDER=${JMETER_HOME}/lib/ext/
COPY jmeter-plugins-influxdb2-listener-2.8.jar ${JMETER_PLUGINS_FOLDER}/jmeter-plugins-influxdb2-listener-2.6.jar

RUN mkdir /app
RUN chmod -R a+w  /app
COPY launch.sh /app/launch.sh
RUN chmod a+x /app/launch.sh
COPY google.jmx /app/google.jmx

WORKDIR ${JMETER_HOME}

ENTRYPOINT ["/app/launch.sh"]