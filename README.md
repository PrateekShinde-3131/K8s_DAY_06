# K8s_DAY_06
# KIND (Kubernetes in Docker) Cluster Setup Guide

This guide covers the steps to set up both a single-node and a multi-node KIND cluster on your local machine, along with installing the `kubectl` client. After following this guide, you’ll have a fully functioning Kubernetes cluster running in Docker containers.

---

## Prerequisites

Ensure that Docker is installed on your machine. KIND (Kubernetes in Docker) uses Docker to run the Kubernetes nodes as containers.

---

## Steps to Setup KIND Clusters

### 1. Install KIND

To install KIND, run the following commands:

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

2. Setting Up a Single-Node Cluster (Kubernetes v1.29)

1.Create a Single-Node Cluster
To create a single-node Kubernetes cluster with KIND using Kubernetes version 1.29, run the following command:
kind create cluster --image kindest/node:v1.29.0

2.Verify the Cluster
After the cluster is created, you can verify the node status with:
kubectl get nodes

3.Delete the Cluster
If you no longer need the single-node cluster, delete it by running:
kind delete cluster

3. Setting Up a Multi-Node Cluster (Kubernetes v1.30)
 1.Create Cluster Configuration
 Create a file called kind-config.yaml with the following configuration for a multi-node cluster:
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
name: cka-cluster2
nodes:
  - role: control-plane
  - role: worker
  - role: worker
  - role: worker
 2.Create the Multi-Node Cluster
 Once the configuration is in place, create the multi-node cluster using Kubernetes version 1.30 by running:
kind create cluster --config=kind-config.yaml --image kindest/node:v1.30.0

4. Installing the kubectl Client
 1.Download and Install Kubectl
Download and install the kubectl client using the following commands:
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

5. Set the Context and Verify the Cluster
 1.Set the Current Context
After creating the multi-node cluster, set the current context to the newly created cluster:
kubectl config use-context kind-cka-cluster2

3.Verify KIND Nodes as Docker Containers
Since KIND uses Docker containers to create Kubernetes nodes, you can verify that the nodes are running as containers by executing:
docker ps



