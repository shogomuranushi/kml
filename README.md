# Google Kubernetes Engine (GKE) samples for Machine Learning

## init

```:bash
# setting gcloud
gcloud init

# Update components
gcloud components update
gcloud components update kubectl
```

## setup

```:bash
#Set CLUSTER_NAM and NODE_POOL
clusterName="default"
zone="us-central1-c"

# Create clustor and nodes
# don't custom this
gcloud container clusters create $clusterName --zone $zone --machine-type=g1-small --num-nodes 2 --disk-size 10 --preemptible

# Create other node-pooks
gcloud container node-pools create highcpu --cluster $clusterName --zone $zone \
        --machine-type=n1-standard-1 --disk-size 10 --preemptible \
        --num-nodes 0 --enable-autoscaling --min-nodes=0 --max-nodes=1 \
        --node-taints=node=highcpu:NoSchedule --node-labels=node=highcpu

# Taint is automatically assigned to GPU nodes
# https://cloud.google.com/kubernetes-engine/docs/how-to/gpus?hl=ja#gpu_pool
gcloud container node-pools create gpu-k80-1 --cluster $clusterName --zone $zone \
        --machine-type=custom-4-26624 --accelerator type=nvidia-tesla-k80,count=1 --disk-size 30 --preemptible \
        --num-nodes 0 --enable-autoscaling --min-nodes=0 --max-nodes=1
        --node-labels=node=gpu-k80-1

kubectl apply -f daemonset-preloaded.yaml

# Delete clustor
# gcloud container clusters delete  $clusterName
```

if you want custom to node
- [Jupyter Node](if_you_want_jupyter_node_custom.md)
- [GPU Node](if_you_want_gpu_node_custom.md)

## Next

- show
- up, down
- jupyer
- exec(ssh) to gpu node
- how to custom image

## up, down

```:bash
# Resize default node to down
gcloud container clusters resize default --zone $zone --num-nodes=0 --node-pool=default-pool --quiet

# Resize default node to up
gcloud container clusters resize default --zone $zone --num-nodes=2 --node-pool=default-pool --quiet
```

## show

```:bash
# Show clustor
gcloud container node-pools list --cluster $clusterName  --zone $zone

# Show credentials
gcloud container clusters get-credentials $clusterName --zone $zone

# Show token
kubectl describe secrets

# Show all pod
kubectl get pod --all-namespaces

# Show all node
kubectl get node

# Show all node-pools
gcloud container node-pools list --cluster $clusterName --zone $zone
```
