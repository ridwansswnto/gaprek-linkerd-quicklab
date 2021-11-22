# Linkerd QuickLab

## Prerequisites

1. Kubernetes (installed locally with minikube)
```
brew install minikube
brew install virtualbox
```


## Deploy a Sample Application

![Emojivoto Topology](emojivoto.png "Emojivoto Topology")


1. Deploy sample apps EMOJIVOTO

```
curl -sL https://run.linkerd.io/emojivoto.yml | kubectl apply -f -
kubectl -n emojivoto port-forward svc/web-svc 8080:80
```

## Deploy Linkerd

1. Install Linkerd

```
curl https://run.linkerd.io/install | sh
export PATH=$PATH:/Users/ridwansiswanto/.linkerd2/bin
linkerd check --pre
linkerd install | kubectl apply -f -
linkerd check
linkerd dashboard

linkerd viz check
linkerd viz dashboard
linkerd viz install | kubectl apply -f -

kubectl get pods -n linkerd
kubectl get pods -n linkerd-viz
```

## Inject Linkerd proxy into the sample application

1. Inject Linkerd Proxy to EMOJIVOTO

```
kubectl get -n emojivoto deploy -o yaml \
 | linkerd inject - \
 | kubectl apply -f -
```
```
linkerd -n emojivoto check --proxy
```
