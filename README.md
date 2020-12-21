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

**You can skip the ArgoCD step and manually deploy the components CRs one by one using oc apply for each of the operator resources**

## Pre-reqs

### Openshift cluster
1- Create an admins group:

   `oc adm groups new admins cluster-manager`
   
   Or apply the file admins-group.yml:
   
   `oc apply -f config/admin-group.yml`
   
2- Assign cluster-admin role to the newly created group and ArgoCD Service Account:

   `oc adm policy add-cluster-role-to-group cluster-admin admins`
   
   Or apply the file cluster-admin-rolebinding.yml:
   
   `oc apply -f config/cluster-admin-rolebinding.yml`

### ArgoCD installation and configuration

#### Installation
You can either install ArgoCD from the OperatorHub menu in Openshift Console (UI)
Or you can go ahead and depoy it using the files in argocd-operator  directory:

`oc apply -f argocd-operator/0-argocd-project.yml`

`oc apply -f argocd-operator/1-argocd-operator-group.yml`

`oc apply -f argocd-operator/2-argocd-subscription.yml`

Switch to argocd project where we will create all our argo artifacts:

`oc project argocd`

Once the operator is installed go ahead and create ArgoCD instance:

`oc apply -f argocd-operator/4-argocd-basic-instance.yml`

This will create an argo instance using openshift OAuth Server so you can login with your openshift credentials.
It also creates 3 Argo CD role assignments:
1- admins
2- deveopers (Not used)
3- marketing (Not used)

**NOTE:** You can totally skip ArgoCD installation if you have your own instance, or you can just deploy manually from the provided CR files for each component.

#### Configuration
We will create a separate Argo Project for cluster amanagement that will be used as the project for all our component apps.

`oc apply -f argo/project.yml`

## Secrets Management
**TODO** Sealed Secret is a the tool of choice to manage secrets so secret is encrypted and stored safely in a GitOps repo.

## Components

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

## References:
1- https://github.com/christianh814/openshift-cluster-config
