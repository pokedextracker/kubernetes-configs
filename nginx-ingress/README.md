# Nginx Ingress

The [nginx ingress controller](https://github.com/kubernetes/ingress-nginx) is
written by the Kubernetes team and is a basic [ingress
controller](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)
powered by [nginx](https://www.nginx.com/).

## Install

```sh
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
kubectl create ns nginx-ingress
helm upgrade \
  --install \
  --wait \
  --namespace nginx-ingress \
  --set controller.replicaCount=2 \
  --set controller.stats.enabled=true \
  --set controller.metrics.enabled=true \
  --set-string controller.config.use-proxy-protocol=true \
  --set controller.extraArgs.default-ssl-certificate=default/wildcard \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/aws-load-balancer-proxy-protocol"='*' \
  nginx-ingress \
  ingress-nginx/ingress-nginx
```
