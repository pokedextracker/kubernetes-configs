# Ghost Blog

[Ghost](https://ghost.org/) powers the [PokédexTracker
blog](https://pokedextracker.com/blog/).

## Install

```sh
$ kubectl apply -f ghost/staging
$ kubectl apply -f ghost/production
```

## Update

```sh
# scale up to reduce downtime
$ kubectl scale deployment ghost --replicas 2 -n staging
# wait for new pod to become ready
$ kubectl apply -f ghost/staging
# wait for pods to cycle out
$ kubectl scale deployment ghost --replicas 1 -n staging

# scale up to reduce downtime
$ kubectl scale deployment ghost --replicas 2 -n production
# wait for new pod to become ready
$ kubectl apply -f ghost/production
# wait for pods to cycle out
$ kubectl scale deployment ghost --replicas 1 -n production
```
