# Cheatsheet: Create k8s cluster

## [Google Cloud](https://cloud.google.com/)

1. Log in to https://console.cloud.google.com
2. Enable the [Container Engine API](https://console.cloud.google.com/apis/api/container.googleapis.com/overview).
3. Install [gcloud SDK](https://cloud.google.com/sdk/downloads)
4. From terminal:

    ```bash
    # Install kubectl
    gcloud components install kubectl

    # create a K8s cluster on Google Cloud
    gcloud container clusters create <YOUR_CLUSTER> \
        --num-nodes=3 \
        --machine-type=n1-standard-2 \
        --zone=us-central1-b

    # test if your cluster is initialized
    kubectl get node

    # give your account super-user permissions
    kubectl create clusterrolebinding cluster-admin-binding \
        --clusterrole=cluster-admin \
        --user=<your-email-address>
    ```

## Microsoft Azure

1. Install and initialize the **Azure command-line tools** from
   [azure-cli github repo](https://github.com/Azure/azure-cli).

2. From terminal:

    ```bash
    # authenticate azure account
    az login

    # specify an Azure resource group and create if needed
    # if needed, view valid locations: az account list-locations
    export RESOURCE_GROUP=<YOUR_RESOURCE_GROUP>
    export LOCATION=<YOUR_LOCATION>
    az group create --name=${RESOURCE_GROUP} --location=${LOCATION}

    # install kubectl
    az acs kubernetes install-cli

    # create k8s cluster
    export CLUSTER_NAME=<YOUR_CLUSTER_NAME>
    export DNS_PREFIX=<YOUR_PREFIX>
    az acs create --orchestrator-type=kubernetes \
      --resource-group=${RESOURCE_GROUP} \
      --name=${CLUSTER_NAME} \
      --dns-prefix=${DNS_PREFIX}

    # authenticate kubectl
    az acs kubernetes get-credentials \
      --resource-group=${RESOURCE_GROUP} \
      --name=${CLUSTER_NAME}

    # test if your cluster is initialized
    kubectl get node
    ```
