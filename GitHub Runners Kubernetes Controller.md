# Kubernetes GitHub Runners

[This is the guide I'm using](https://github.com/actions-runner-controller/actions-runner-controller)

## Steps taken

We need to install cert-manager on the cluster to
authenticate [Admission Webhooks](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#what-are-admission-webhooks)

On Turing run the following commands against the Kubernetes cluster:

`kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.6.1/cert-manager.yaml`

`kubectl apply -f https://github.com/actions-runner-controller/actions-runner-controller/releases/download/v0.20.2/actions-runner-controller.yaml`

I created a new App in github to use:

https://github.com/settings/apps/self-hosted-kubernetes-runners

Last thing was to make a new Dockerfile that the runners will use and create some deployments.