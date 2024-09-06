# K8s_DAY_06
# KIND (Kubernetes in Docker) Cluster Setup Guide

This guide will walk you through the steps to set up both single-node and multi-node KIND clusters on your local machine. You will also install the `kubectl` client to manage the cluster and verify that everything is running correctly.

---

## Prerequisites

Before you start, make sure you have Docker installed on your local machine. KIND (Kubernetes in Docker) uses Docker containers to simulate Kubernetes nodes.

---

## 1. Installing a Single-Node KIND Cluster

### Step 1: Install KIND
To install KIND on your local machine, run the following commands:
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

 Step 2: Create a Single-Node Cluster (Kubernetes v1.29)
Create a single-node cluster using KIND with Kubernetes version 1.29:

kind create cluster --image kindest/node:v1.29.0

 Step 3: Delete the Cluster
To delete the single-node cluster, run the following command:

kind delete cluster

 ## 2. Installing a Multi-Node KIND Cluster
 Step 1: Create a Cluster Configuration

To create a multi-node KIND cluster, you need a configuration file. Create a file called kind-config.yaml with the following content:
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
name: cka-cluster2
nodes:
  - role: control-plane
  - role: worker
  - role: worker
  - role: worker

 Step 2: Create the Multi-Node Cluster (Kubernetes v1.30)
Once the configuration is in place, create the cluster with Kubernetes version 1.30:
kind create cluster --config=kind-config.yaml --image kindest/node:v1.30.0

 3. Installing the kubectl Client
 Step 1: Install Kubectl
Download and install the kubectl client to manage your Kubernetes clusters:
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

 4. Set the Current Context and Verify the Cluster
 Step 1: Set the Context to the Multi-Node Cluster
To switch the context to the newly created multi-node cluster, use the following command:
kubectl config use-context kind-cka-cluster2

 Step 2: Verify the Nodes
To ensure that the control plane and worker nodes are running, use this command:
kubectl get nodes

 Step 3: Verify KIND Nodes as Docker Containers
Since KIND creates Kubernetes nodes as Docker containers, you can check if the containers are running with:
docker ps


