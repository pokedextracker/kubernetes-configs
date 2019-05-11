# Cert Manager

[Cert Manager](https://github.com/jetstack/cert-manager) is used to create TLS
certificates through [Let's Encrypt](https://letsencrypt.org/).

## Install

```sh
$ kubectl apply -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.7/deploy/manifests/00-crds.yaml
$ helm repo add jetstack https://charts.jetstack.io
$ helm repo update
$ helm upgrade \
  --install \
  --wait \
  --namespace cert-manager \
  --version v0.7.0 \
  --set 'podAnnotations.iam\.amazonaws\.com/role=kubernetes-pokedextracker-cert-manager' \
  cert-manager \
  jetstack/cert-manager

# create issuers and certificates
$ kubectl apply -f cert-manager/staging-cluster-issuer.yaml
$ kubectl apply -f cert-manager/staging-wildcard.yaml
# make sure both become Ready=True
$ kubectl apply -f cert-manager/production-cluster-issuer.yaml
$ kubectl apply -f cert-manager/production-wildcard.yaml
```
