FROM amazonlinux:2018.03-with-sources

LABEL maintainer="brandon@papworth.me"
LABEL org.label-schema.description="An Amazon Linux container with Node.js, npm, yarn, and some build tools installed."
LABEL org.label-schema.vcs-url="https://github.com/brandonpapworth/docker-node-amazonlinux"

# Ensure build tools are present for native module compilation
RUN yum -y update \
 && yum -y groupinstall "Development Tools" \
 && yum -y install python27-devel \
 && curl -sL https://bootstrap.pypa.io/get-pip.py | python \
 && pip install awscli \
 && yum clean all

ENV PATH="${PATH}:/root/.local/bin"

# See https://github.com/nodesource/distributions#rpm
RUN pip install --user aws-sam-cli \
 && curl -sL https://rpm.nodesource.com/setup_8.x | bash - \
 && yum -y update \
 && yum -y install nodejs \
 && curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo \
 && yum -y update \
 && yum -y install yarn \
 && yum clean all \
 && npm install -g aws-sdk
