FROM java:8-jdk

ENV ELASTIC_VERSION=6.1.3
ENV METRICBEAT_URL=https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-${ELASTIC_VERSION}-linux-x86_64.tar.gz
ENV METRICBEAT_HOME=/opt/metricbeat-linux-x86_64

RUN mkdir $METRICBEAT_HOME && \
    curl -sL ${METRICBEAT_URL} | tar xz -C $METRICBEAT_HOME --strip-components=1
COPY metricbeat.yml $METRICBEAT_HOME/metricbeat.yml

ENV FILEBEAT_URL=https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${ELASTIC_VERSION}-linux-x86_64.tar.gz
ENV FILEBEAT_HOME=/opt/filebeat-linux-x86_64

RUN mkdir $FILEBEAT_HOME && \
    curl -sL ${FILEBEAT_URL} | tar xz -C $FILEBEAT_HOME --strip-components=1
COPY filebeat.yml $FILEBEAT_HOME/filebeat.yml

COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

RUN mkdir /app
WORKDIR /app
COPY target/tnt-ms-catalog-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8081

#ENV DOCKERIZE_VERSION v0.2.0
#RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
#    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz
# "dockerize", "-timeout", "5m", "-wait", "http://config-server:8100/health",