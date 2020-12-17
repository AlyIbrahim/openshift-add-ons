# openshift-add-ons
This project is aimed to managing add-on features on top of openshift in a GitOps Declarative way using ArgoCD to deploy and manage day 2 add-on services like Serverless, Strimzi, Service Mesh, etc. on top of a new installed openshift cluster.
This project is aimed to demo environment, though the same concept and configuration can be applied to customer environments

## Solution Components
- Openshift : We try to adhere to the latest as possible
- ArgoCD    : 
  - We use the latest ArgoCD delivered through the openshift Operator Hub, but feel free to use your own instance of ArgoCD
  - ArgoCD admin in this repo has a cluster-admin role to create namespaces and delete resources, this can change and PRs are welcomed.
  - We create a spcific ArgoCD Project for the purpose of cluster-management
  - We have an ArgoCD App for each of the components to make it easy to deploy the whole thing in one shot
  
The solution is currently based on ArgoCD, we may extend this to other tools in the future.
** You can skip the ArgoCD step and manually deploy the components CRs one by one using oc apply for each of the operator resources **

## Pre-reqs

## Installation

## Secrets Management

## Components

### ArgoCD

### Advanced Cluster Management

### AMQ Streams (Kafka Strimzi)

### Service Mesh

### Serverless (Knative)

### Pipelines (Tekton)

### CodeReady Workspaces

### Jenkins

### Quay

## Configuration
The configuration of each of these add-ons is as close to the default as possible, feel free to send PRs for your prefered common configuration that you wish to have and also feel free to fork the repo for your own specific configuration.
