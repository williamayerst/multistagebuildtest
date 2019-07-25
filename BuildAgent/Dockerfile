FROM jenkinsci/jnlp-slave
LABEL Mainteiner="William Ayerst <@wayerst>"

ENV DOCKER_VERSION=17.04.0-ce DOCKER_COMPOSE_VERSION=1.14.0
# ENV DOCKER_VERSION=17.04.0-ce DOCKER_COMPOSE_VERSION=1.14.0 KUBECTL_VERSION=v1.6.6

USER root


# Install Dotnet
RUN apt-get install software-properties-common  -y -qq --no-install-recommends \
    && add-apt-repository "deb http://archive.ubuntu.com/ubuntu xenial universe" \
    && apt-get update  -qq \
    && apt-get install apt-transport-https -y -qq --no-install-recommends 

# Add MS Key and install dependencies
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb

# Install Dotnet
RUN apt-get install dotnet-sdk-2.2

# Update image
RUN apt-get update -qq && apt-get install -y -qq --no-install-recommends \
    make \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install AZCLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install Docker
RUN curl -fsSLO https://get.docker.com/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz \
		&& tar --strip-components=1 -xvzf docker-${DOCKER_VERSION}.tgz -C /usr/local/bin \
		&& chmod -R +x /usr/local/bin/docker

# Install Kubectl
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
    && echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list \
    && apt-get update

# Install Kubectl (oldschool)
# RUN curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
#   && chmod +x /usr/local/bin/kubectl

# Install Kustomize
RUN wget -O $KustomizeBinaryPath $KustomizeDownloadPath && chmod +x $KustomizeBinaryPath \
    && $KustomizeBinaryPath version
