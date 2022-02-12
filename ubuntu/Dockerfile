FROM summerwind/actions-runner:latest

RUN sudo apt-get update \
    && sudo apt-get install -y apt-transport-https ca-certificates curl

# install Kubernetes
RUN sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg

RUN echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

RUN sudo apt-get update \
    && sudo apt-get install -y kubectl

# install Ansible
RUN sudo apt-get update \
    && sudo apt-get install -y software-properties-common

RUN sudo add-apt-repository --yes --update ppa:ansible/ansible

RUN sudo apt-get install -y  ansible

RUN sudo rm -rf /var/lib/apt/lists/*

# Install Galaxy roles
RUN ansible-galaxy install geerlingguy.docker, geerlingguy.kubernetes