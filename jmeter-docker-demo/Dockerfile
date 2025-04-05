# Stage 1 - Builder
FROM eclipse-temurin:17-jdk as builder

ARG JMETER_VERSION=5.6.3
ARG JMETER_HOME=/opt/apache-jmeter-${JMETER_VERSION}

RUN apt-get update && apt-get install -y curl unzip && \
    curl -sL https://downloads.apache.org//jmeter/binaries/apache-jmeter-${JMETER_VERSION}.zip -o /tmp/jmeter.zip && \
    unzip /tmp/jmeter.zip -d /opt && \
    rm /tmp/jmeter.zip

# Stage 2 - Runtime (minimal)
FROM eclipse-temurin:17-jre

ARG JMETER_VERSION=5.6.3
COPY --from=builder /opt/apache-jmeter-${JMETER_VERSION} /opt/apache-jmeter

ENV JMETER_HOME /opt/apache-jmeter
ENV PATH $JMETER_HOME/bin:$PATH

WORKDIR /opt/apache-jmeter
ENTRYPOINT ["jmeter"]
