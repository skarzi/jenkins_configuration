FROM jenkins/jenkins:2.232

ARG JAVA_OPTS

ENV JENKINS_HOME=/var/jenkins_home \
    JAVA_OPTS="-Djenkins.install.runSetupWizard=false ${JAVA_OPTS:-}" \
    JENKINS_PLUGINS_FILE=/usr/share/jenkins/ref/plugins_extra.txt

COPY docker/master/plugins_extra.txt "${JENKINS_PLUGINS_FILE}"

RUN xargs /usr/local/bin/install-plugins.sh < "${JENKINS_PLUGINS_FILE}"
