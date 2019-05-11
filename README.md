# Kubernetes Configs

This repo contains Helm `values.yaml`s and raw Kubernetes YAML files used to
bootstrap the PokédexTracker Kubernetes cluster.

## Order

This is the order that these components need to be applied.

1. Create cluster
2. Install Tiller/Helm
3. Install kube2iam
4. Install Cert Manager
5. Install nginx Ingress
6. Install Datadog Agent
7. Deploy applications
    1. Backend (in [dedicated repo](https://github.com/pokedextracker/api.pokedextracker.com))
    2. Frontend (in [dedicated repo](https://github.com/pokedextracker/pokedextracker.com))
    3. Blog (ghost)
