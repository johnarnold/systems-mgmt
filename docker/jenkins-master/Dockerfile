FROM jenkins
MAINTAINER user

USER root
RUN mkdir /var/log/jenkins
RUN mkdir /var/cache/jenkins
RUN chown -R  jenkins:jenkins /var/log/jenkins
RUN chown -R jenkins:jenkins /var/cache/jenkins


# install plugins; the plugins.txt file can be exported from Jenkins like this:
# JENKINS_HOST=username:password@myhost.com:port
# curl -sSL "http://$JENKINS_HOST/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version

# NOTE : Just set pluginID to download latest version of plugin.
# NOTE : All plugins need to be listed as there is no transitive dependency resolution.
#COPY plugins.txt /usr/share/jenkins/plugins.txt
#RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

# Alternative to plugins.sh which does dependency resolution:
RUN install-plugins.sh ace-editor \
active-directory \
analysis-collector \
analysis-core \
ansicolor \
ant \
antisamy-markup-formatter \
authentication-tokens \
backup \
bouncycastle-api \
branch-api \
build-environment \
clang-scanbuild-plugin \
cloudbees-folder \
cobertura \
conditional-buildstep \
config-file-provider \
copyartifact \
cppcheck \
credentials \
credentials-binding \
cvs \
dashboard-view \
display-url-api \
docker-commons \
docker-plugin \
docker-traceability \
docker-workflow \
durable-task \
embeddable-build-status \
extended-read-permission \
external-monitor-job \
ghprb \
git \
git-changelog \
git-client \
git-parameter \
git-server \
github \
github-api \
github-branch-source \
github-oauth \
github-organization-folder \
github-pullrequest \
handlebars \
icon-shim \
javadoc \
jobConfigHistory \
jquery \
jquery-detached \
junit \
ldap \
log-parser \
mailer \
mapdb-api \
matrix-auth \
matrix-project \
maven-plugin \
momentjs \
pam-auth \
parameterized-trigger \
pipeline-build-step \
pipeline-graph-analysis \
pipeline-input-step \
pipeline-milestone-step \
pipeline-rest-api \
pipeline-stage-step \
pipeline-stage-view \
plain-credentials \
run-condition \
scm-api \
script-security \
scripttrigger \
simple-theme-plugin \
ssh \
ssh-agent \
ssh-credentials \
ssh-slaves \
structs \
subversion \
tasks \
thinBackup \
token-macro \
translation \
violations \
warnings \
windows-slaves \
workflow-aggregator \
workflow-api \
workflow-basic-steps \
workflow-cps \
workflow-cps-global-lib \
workflow-durable-task-step \
workflow-job \
workflow-multibranch \
workflow-scm-step \
workflow-step-api \
workflow-support


# NOTE: This indicates that this Jenkins installation is fully configured. Otherwise a banner will appear prompting the user to install additional plugins
RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state

USER jenkins

ENV JAVA_OPTS="-Xmx8192m"
ENV JENKINS_OPTS="--handlerCountMax=300 --logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkins/war"

