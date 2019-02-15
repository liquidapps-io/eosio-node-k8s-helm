# Deploying a EOSIO mainnet API node

Sets up a full EOSIO node and syncs from the latest available blocks log backup and snapshot.

## Getting started
### AWS
https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html

### GCP
https://cloud.google.com/kubernetes-engine/docs/quickstart

## Deployment using helm
### Install helm

Download client from: https://docs.helm.sh/using_helm/#installing-helm
#### Ubuntu
```
sudo snap install helm --classic
```

Run:
```
helm init
helm update repo

kubectl create serviceaccount --namespace kube-system tiller 
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller 
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'

```
### Install the EOSIO node helm chart
```
git clone https://github.com/liquidapps-io/eosio-node-k8s-helm.git
cd eosio-node-k8s-helm
helm install --set snapshot=true --set replay=true .

```

