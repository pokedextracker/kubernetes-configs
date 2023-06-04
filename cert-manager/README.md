# Cert Manager

[Cert Manager](https://github.com/jetstack/cert-manager) is used to create TLS
certificates through [Let's Encrypt](https://letsencrypt.org/).

## Install

```sh
kubectl create namespace cert-manager
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm upgrade \
  --install \
  --wait \
  --namespace cert-manager \
  --version v0.15.0 \
  --set 'podAnnotations.iam\.amazonaws\.com/role=kubernetes-pokedextracker-<hash>-cert-manager' \
  --set installCRDs=true \
  cert-manager \
  jetstack/cert-manager

# create issuers and certificates
kubectl apply -f cert-manager/staging-cluster-issuer.yaml
kubectl apply -f cert-manager/staging-wildcard.yaml
while [ 1 ]; do kubectl get certificates staging-wildcard -n default -o json | jq '.status'; sleep 5; done
# make sure both become Ready=True
kubectl apply -f cert-manager/production-cluster-issuer.yaml
kubectl apply -f cert-manager/production-wildcard.yaml
while [ 1 ]; do kubectl get certificates wildcard -n default -o json | jq '.status'; sleep 5; done
```
