# Cilium Intro

![](./logo.png)

You can find the related blog here:
- 中文版：[wordpress]()
- English Version: TODO

## Installation
  
```bash
kubectl apply ./cilium/install-v1.7.1.yaml

```

## Component list

```bash
> kubectl get all --all-namespaces |grep cilium
kube-system     pod/cilium-89ncn                                            1/1     Running            0          27h
kube-system     pod/cilium-9f9dn                                            1/1     Running            1          25h
kube-system     pod/cilium-hjd7t                                            1/1     Running            0          27h
kube-system     pod/cilium-operator-6547f48966-r4mqp                        1/1     Running            0          27h
kube-system     pod/cilium-pg5lp                                            1/1     Running            0          25h
kube-system     daemonset.apps/cilium              4         4         4       4            4           <none>                        27h
kube-system     deployment.apps/cilium-operator                         1/1     1            1           27h
kube-system     replicaset.apps/cilium-operator-6547f48966                        1         1         1       27h
```

## Check Cilium availability

We can use the official tool to check the connectivity after the installation.

```shell
kubectl apply -f ./cilium/connectivity-check.yaml
```  

## Try Cilium Hubble

```shell

git clone https://github.com/cilium/hubble.git
cd hubble/install/kubernetes

helm template hubble \
    --namespace kube-system \
    --set metrics.enabled="{dns:query;ignoreAAAA;destinationContext=pod-short,drop:sourceContext=pod;destinationContext=pod,tcp,flow,port-distribution,icmp,http}" \
    --set ui.enabled=true \
    > hubble.yaml

kubectl apply -f hubble.yaml

# create a nodeport service for hubble ui to access externally
kubectl apply -f hubble-ui-nodeport.yaml
```

## Compare with Calico

TODO
