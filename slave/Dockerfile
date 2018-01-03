# The FROM will be replaced when building in OpenShift
FROM openshift/jenkins-slave-base-centos7

MAINTAINER Siamak Sadeghianfar <ssadeghi@redhat.com>

ENV MAVEN_VERSION=3.3 \
    GRADLE_VERSION=4.2.1 \
    BASH_ENV=/usr/local/bin/scl_enable \
    ENV=/usr/local/bin/scl_enable \
    PROMPT_COMMAND=". /usr/local/bin/scl_enable" \
    PATH=$PATH:/opt/gradle/bin

# Install Maven
RUN INSTALL_PKGS="java-1.8.0-openjdk-devel.x86_64 java-1.8.0-openjdk-devel.i686 rh-maven33*" && \
    yum install -y centos-release-scl-rh && \
    yum install -y --enablerepo=centosplus $INSTALL_PKGS && \
    curl -LOk https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip gradle-${GRADLE_VERSION}-bin.zip -d /opt && \
    rm -f gradle-${GRADLE_VERSION}-bin.zip && \
    ln -s /opt/gradle-${GRADLE_VERSION} /opt/gradle && \
    rpm -V ${INSTALL_PKGS//\*/} && \
    yum clean all -y && \
    mkdir -p $HOME/.m2 && \
    mkdir -p $HOME/.gradle && \
    chmod -R 777 /usr/local/bin && \
    curl -SsL https://downloads.getgauge.io/stable | sh && \
    gauge install java


RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
