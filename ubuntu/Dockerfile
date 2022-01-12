FROM debian:buster

ARG GH_ACTIONS_RUNNER_VERSION=2.283.1
ARG PACKAGES="gnupg2 apt-transport-https ca-certificates software-properties-common pwgen git make curl wget zip libicu-dev build-essential libssl-dev jq dos2unix sudo"
ARG GH_PAT_TOKEN
ARG KUBECONFIG

ENV GITHUB_PAT=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

# install basic stuff
RUN apt-get update \
    && apt-get install -y -q ${PACKAGES} \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# install docker
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && apt-key fingerprint 0EBFCD88 \
    && add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) \
       stable" \
    && apt-get update \
    && apt-get install -y docker-ce-cli \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# install Kubernetes
RUN curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg

RUN echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | tee /etc/apt/sources.list.d/kubernetes.list

RUN apt-get update && apt-get install -y kubectl

# install Ansible
RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu bionic main" | tee -a /etc/apt/sources.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367

RUN apt-get update && apt-get install -y ansible

# create "runner" user
RUN useradd -d /runner --uid=1000 runner \
    && echo 'runner:runner' | chpasswd \
    && mkdir /runner \
    && chown -R runner:runner /runner

WORKDIR /runner

COPY entrypoint.sh /runner

CMD /runner/entrypoint.sh