FROM node:22-bookworm-slim

# Defining default Java and Maven version
ARG JAVA_VERSION="11.0.25-amzn"
ARG SBT_VERSION="1.10.1"

# Installing SDKMAN! dependencies
RUN apt-get update && \
	apt-get install -y zip unzip curl && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /tmp/*

# Install CDK CLI
RUN npm install -g aws-cdk

# Downloading SDKMAN!
RUN curl -s "https://get.sdkman.io" | bash

# Create AWS config and workspace directories
RUN mkdir -p /root/.aws

# Installing Java and SBT, removing some unnecessary SDKMAN files
RUN bash -c "source $HOME/.sdkman/bin/sdkman-init.sh && \
    yes | sdk install java $JAVA_VERSION && \
    yes | sdk install sbt $SBT_VERSION && \
    rm -rf $HOME/.sdkman/archives/* && \
    rm -rf $HOME/.sdkman/tmp/*"

# Setup PATH env variable for SBT and Java
ENV PATH=$PATH:/root/.sdkman/candidates/sbt/$SBT_VERSION/bin:/root/.sdkman/candidates/java/$JAVA_VERSION/bin
ENV JAVA_HOME=/root/.sdkman/candidates/java/$JAVA_VERSION

