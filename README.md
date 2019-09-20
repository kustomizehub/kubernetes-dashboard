# kubernetes-dashboard

This repo contains kustomize manifest for [kubernetes-dashboard](https://github.com/kubernetes/dashboard)

## How to use

Download the repo:

``` bash
git clone https://github.com/kustomizehub/kubernetes-dashboard.git
```

### Default installation

``` bash
kubectl create namespace kubernetes-dashboard
kustomize build kubernetes-dashboard/base | kubectl apply -f -
```

- Autogenerate self-signed certificates
- in kubernetes-dashboard namespace

### Customize certificates

Prepare namespace:

``` bash
kubectl create namespace kubernetes-dashboard
```

Prepare your certificates:

- Secret name: `kubernetes-dashboard-certs`.
- Secret content: `tls.crt` is the cert, `tls.key` is the private key.

apply:

``` bash
kustomize build kubernetes-dashboard/certs | kubectl apply -f -
```

### Customize namespace

Prepare your own `kustomization.yaml`，

``` yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
# reference the configuration dir you want to override
bases:
- ./kubernetes-dashboard/base
#- ./kubernetes-dashboard/certs
namespace: dashboard
```

Prepare namespace:

``` bash
kubectl create namespace dashboard
```

apply:

``` bash
kustomize build . | kubectl apply -f -
```

## LICENSE

MIT