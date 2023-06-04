# Blog

Our blog is currently hosted by [Midnight](https://getmidnight.com/), but we
want the domain for our blog to be `https://pokedextracker.com/blog/`, so we
set up an NGINX reverse proxy to our Midnight domain.

## Install

```sh
kubectl apply -f blog/manifests.yaml
```
