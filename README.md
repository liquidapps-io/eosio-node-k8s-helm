# EOSIO Mainnet full node deployment using K8s and helm

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
### Clone the EOSIO node helm chart
```bash
git clone https://github.com/liquidapps-io/eosio-node-k8s-helm.git
cd eosio-node-k8s-helm
```

### Run
Restore from snapshot:
```bash
helm install --set snapshot=true . --name nodeos
```
Or restore from full backup and replay:
```bash
helm install --set snapshot=true --set replay=true . --name nodeos
```
Or resume after first restore:
```bash
helm install . --name nodeos
```