FROM base:latest

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
      curl \
      openssh-client \
      openjdk-11-jre

RUN mkdir -p /var/gerrit/bin && \
    mkdir -p /var/gerrit/etc && \
    mkdir -p /var/gerrit/plugins && \
    mkdir -p /var/plugins && \
    mkdir -p /var/war

# Download Gerrit release
ARG GERRIT_WAR_URL=https://gerrit-releases.storage.googleapis.com/gerrit-3.3.1.war
RUN curl -k -o /var/war/gerrit.war ${GERRIT_WAR_URL} && \
    ln -s /var/war/gerrit.war /var/gerrit/bin/gerrit.war

# Download healthcheck plugin
RUN curl -k -o /var/plugins/healthcheck.jar \
        https://gerrit-ci.gerritforge.com/job/plugin-healthcheck-bazel-stable-3.3/lastSuccessfulBuild/artifact/bazel-bin/plugins/healthcheck/healthcheck.jar && \
    ln -s /var/plugins/healthcheck.jar /var/gerrit/plugins/healthcheck.jar

# Download checks plugin
RUN curl -k -o /var/plugins/checks.jar \
        https://gerrit-ci.gerritforge.com/job/plugin-checks-bazel-stable-3.3/lastSuccessfulBuild/artifact/bazel-bin/plugins/checks/checks.jar && \
    ln -s /var/plugins/checks.jar /var/gerrit/plugins/checks.jar

# Allow incoming traffic
EXPOSE 29418 8080

RUN chown -R gerrit:users /var/gerrit && \
    chown -R gerrit:users /var/plugins && \
    chown -R gerrit:users /var/war
USER gerrit

# RUN java -jar /var/gerrit/bin/gerrit.war init \
#       --batch \
#       --no-auto-start \
#       -d /var/gerrit

ENTRYPOINT ["ash", "/var/tools/start"]
