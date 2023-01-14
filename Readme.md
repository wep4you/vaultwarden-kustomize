# Bitwarden Password Manager

Password Manager from Original Source -> At the moment no ARM Support!

## Sources
* https://github.com/bitwarden/server
* https://hub.docker.com/r/bitwarden/server

* https://github.com/dani-garcia/vaultwarden
* https://hub.docker.com/r/vaultwarden/server



## Setup Sealed Secret for Maria-DB
Choose the right directory, where your own overlay lives, for example `overlays/local`

```zsh
kubectl --namespace vaultwarden create secret generic mariadb --dry-run=client \
    --from-literal mariadb-root-password='<YOUR-PASSWORD>' \
    --from-literal mariadb-password='<YOUR-PASSWORD>' \
    --output json | kubeseal | tee overlays/local/mariadb/sealedsecret.yml
```

## Install with Argo CD

Use a central repository which links to all Apps which has to be deployed,
and add the App desciption there, or deploy the App for Uptime Kuma manually.
Find a sample in my [App of Apps Repo](https://github.com/wep4you/k8s-apps.git),
there is also a sample definition for [Vaultwarden](https://github.com/wep4you/k8s-apps/blob/main/local/vaultwarden.yml)

## Install manual with kubectl

To add your own configuration, copy `overlays/local` to a new folder and change the files to your needs.
It's standard Kustomize format you can use.

```shell
kubectl apply -k overlays/local
```
