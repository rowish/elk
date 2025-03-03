FROM docker.elastic.co/logstash/logstash:${STACK_VERSION}

# Switch to Logstash directory
WORKDIR /usr/share/logstash

# Ensure keystore exists
RUN bin/logstash-keystore create

# Add secrets to the keystore (values must be passed as build arguments or set later)
ARG SMTP_USER
ARG SMTP_PASSWORD

RUN echo "$SMTP_USER" | bin/logstash-keystore add SMTP_USER --stdin && \
    echo "$SMTP_PASSWORD" | bin/logstash-keystore add SMTP_PASSWORD --stdin

# Ensure the keystore file is owned by the Logstash user
RUN chown logstash:logstash config/logstash.keystore

USER logstash
