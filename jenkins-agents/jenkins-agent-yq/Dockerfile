FROM quay.io/openshift/origin-jenkins-agent-base:4.4

ARG YQ_VERSION=3.3.0
ARG OPENSHIFT_CLIENT_VERSION=4.4.13

## Required in order to avoid ct "ascii codec can't encode character" error
ENV PYTHONIOENCODING=utf-8

## Install helm and yq
RUN curl -sL  https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64 -o /usr/local/bin/yq && \
    chmod -R 775 /usr/local/bin/yq

## Install oc and kubectl
RUN curl -s https://mirror.openshift.com/pub/openshift-v4/clients/ocp/${OPENSHIFT_CLIENT_VERSION}/openshift-client-linux-${OPENSHIFT_CLIENT_VERSION}.tar.gz \
    | tar zxf - -C /usr/local/bin oc kubectl 

## Persistently enable software collections
RUN mkdir /usr/share/container-scripts
COPY scl_enable /usr/share/container-scripts
RUN chmod 555 /usr/share/container-scripts/scl_enable
ENV BASH_ENV=/usr/share/container-scripts/scl_enable \
    ENV=/usr/share/container-scripts/scl_enable \
    PROMPT_COMMAND=". /usr/share/container-scripts/scl_enable"

USER 1001
