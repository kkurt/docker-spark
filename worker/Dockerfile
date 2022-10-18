FROM kkurt/spark3cluster

LABEL maintainer="Kursat Kurt <kursat@kursatkurt.com>"

COPY worker.sh /

ENV SPARK_WORKER_WEBUI_PORT 8081
ENV SPARK_WORKER_LOG /spark/logs
ENV SPARK_MASTER "spark://spark-master:7077"

EXPOSE 8081

## Should be coipe all needed JAR files into sparkJar
COPY cd sparkJars/* ./spark/jars/
CMD ["/bin/bash", "/worker.sh"]
