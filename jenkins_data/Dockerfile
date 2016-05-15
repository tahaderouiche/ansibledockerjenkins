FROM alpine:3.3

ENV JENKINS_HOME /var/jenkins_home

ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000

# Jenkins is run with user `jenkins`, uid = 1000
# If you bind mount a volume from the host or a data container,
# ensure you use the same uid
RUN addgroup -g ${gid} ${group} \
    && adduser -h "$JENKINS_HOME" -u ${uid} -G ${group} -s /bin/bash -D ${user}


RUN mkdir -p /var/log/jenkins
RUN chown -R jenkins:jenkins /var/log/jenkins

# Jenkins home and log directory is a volume, so configuration and build history
# can be persisted and survive image upgrades
VOLUME ["/var/log/jenkins", "/var/jenkins_home"]


USER jenkins

CMD ["echo", "Data container for Jenkins"]

