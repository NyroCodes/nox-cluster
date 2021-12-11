# Setup - Nox Cluster

## Useful commands

```
flux get kustomization -A --watch
```

## Install k3os Server Node

Mount k3os iso and use server.config.yaml as cloud-init file

```
sudo k3os install
```

## Bootstrap fluxcd

```
flux bootstrap github --owner NyroCodes --repository nox-cluster-flux --personal=true
```

## Add sops-age key and ssh-credentials for base-secret

Add sops-age
```
kubectl -n base-secret create secret generic sops-age \
    --from-file=./age.agekey
```

Add ssh-credentials
```
kubectl -n base-secret create secret generic ssh-credentials \
    --from-file=./identity \
    --from-file=./identity.pub \
    --from-file=./known_hosts
```