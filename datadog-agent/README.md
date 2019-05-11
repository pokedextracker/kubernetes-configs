# Datadog Agent

The [Datadog Agent](https://github.com/DataDog/datadog-agent) runs as a
DaemonSet and collects metrics to send to
[Datadog](https://www.datadoghq.com/).

## Install

```sh
$ kubectl create ns datadog-agent
$ kubectl create secret generic datadog-api-key -n datadog-agent --from-literal=api-key=<DATADOG_API_KEY>
$ kubectl apply -f datadog-agent/01-service-account.yaml
$ kubectl apply -f datadog-agent/02-cluster-role.yaml
$ kubectl apply -f datadog-agent/03-cluster-role-binding.yaml
$ kubectl apply -f datadog-agent/04-daemon-set.yaml
```

## Update

```sh
$ kubectl apply -f datadog-agent
```
