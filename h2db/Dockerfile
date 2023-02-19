FROM alpine:3.7
RUN  apk update \
  && apk add --no-cache openjdk8 \
  && rm -rf /var/cache/apk/* \
  && mkdir -p /opt \
  && wget https://github.com/h2database/h2database/releases/download/version-2.1.212/h2-2022-04-09.zip \
  && unzip h2-*.zip \
  && rm -f h2-*.zip \
  && mv h2 /opt \
  && mkdir -p /opt/h2/data
EXPOSE 9092 5435 8082
VOLUME /opt/h2/data
COPY backup.sql .
RUN java -cp /opt/h2/bin/h2-2.1.212.jar org.h2.tools.RunScript -url jdbc:h2:/opt/h2/data/hokkaido -user sa -password "1234" -script backup.sql
CMD ["java", "-cp", "/opt/h2/bin/h2-2.1.212.jar", "org.h2.tools.Server", "-tcp", "-tcpAllowOthers", "-web", "-webAllowOthers", "-pg", "-pgAllowOthers", "-baseDir", "/opt/h2/data"]

