# Login
az login

# Create resource group
az group create --name myResourceGroup --location eastus

# Create AKS cluster with 2 nodes
az aks create \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --node-count 2 \
  --enable-addons monitoring \
  --generate-ssh-keys
# Once your cluster is created, connect it with kubectl:
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster

# Now you can manage it like any Kubernetes cluster:

kubectl get nodes
kubectl get pods -A

# Scaling the Cluster
az aks scale \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --node-count 4
# Enable Auto-scaling
az aks update \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --enable-cluster-autoscaler \
  --min-count 2 \
  --max-count 5
# Upgrading the Cluster
<!-- check version -->
az aks get-upgrades \

  --resource-group myResourceGroup \
  --name myAKSCluster
<!-- upgrade -->
az aks upgrade \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --kubernetes-version 1.29.3
