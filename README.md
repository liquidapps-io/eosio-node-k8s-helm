# Deploying a EOSIO mainnet API node

Sets up a full EOSIO node. and syncs from the latest available blocks log backup.

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
helm repo add liquidapps https://s3-us-west-2.amazonaws.com/liquidapps-helm-charts/
helm update repo

kubectl create serviceaccount --namespace kube-system tiller 
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller 
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'

```
### Install the EOSIO node helm chart
```
wget https://raw.githubusercontent.com/liquidapps-io/eosio-node-k8s-helm/master/values.yaml -O eosnode-config.yaml
# edit eosnode-config.yaml
helm install -f eosnode-config.yaml liquidapps/eosnode

```

