FROM alpine:3.16.2

LABEL maintainer="Kursat Kurt <kursat@kursatkurt.com>"

ENV ENABLE_INIT_DAEMON false
ENV INIT_DAEMON_BASE_URI http://identifier/init-daemon
ENV INIT_DAEMON_STEP spark_master_init

ENV BASE_URL=https://archive.apache.org/dist/spark/
ENV SPARK_VERSION=3.3.0
ENV HADOOP_VERSION=3
ENV SCALA_VERSION=2.13



COPY wait-for-step.sh /
COPY execute-step.sh /
COPY finish-step.sh /


#COPY bde-spark.css /css/org/apache/spark/ui/static/timeline-view.css

RUN apk add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community

#RUN apk add --no-cache curl bash openjdk8-jre python3 py-pip nss libc6-compat coreutils procps \
#RUN apk add curl bash openjdk11-jdk python3 py-pip nss libc6-compat coreutils procps \
RUN apk add curl bash openjdk8-jre python3 py-pip nss libc6-compat coreutils procps \
      && ln -s /lib64/ld-linux-x86-64.so.2 /lib/ld-linux-x86-64.so.2 \
      && chmod +x *.sh \
      && wget "${BASE_URL}/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}-scala${SCALA_VERSION}.tgz" \
      && tar -xvzf "spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}-scala${SCALA_VERSION}.tgz" \
      && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}-scala${SCALA_VERSION} spark \
      && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}-scala${SCALA_VERSION}.tgz \
      #&& cd /css \
      #&& jar uf /spark/jars/spark-core_2.13-${SPARK_VERSION}.jar org/apache/spark/ui/static/timeline-view.css \
      && cd /

#Give permission to execute scripts
RUN chmod +x /wait-for-step.sh && chmod +x /execute-step.sh && chmod +x /finish-step.sh

# Fix the value of PYTHONHASHSEED
# Note: this is needed when you use Python 3.3 or greater
ENV PYTHONHASHSEED 1
