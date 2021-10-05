# Helm Upgrade 

  

## Purpose

the purpose of the composite action is to centralize the code that is used in a single file and avoid misconfiguration and duplicate code.

  

## How to use

  

if this composite action is placed in the repository it with the rest of the workflows see example 1.

if this repository is checked into a public repository see example 2.

  

## parameters

- azure-credentials: credentials to login to Azure
    
    SAMPLE: ${{secrets.AZURE_CREDENTIALS}}
- chart-path: the path to the helm chart

    SAMPLE:  ".helm/<my-chart>"
- azure-subscription: subscription where the cluster is provisioned
  
    SAMPLE:  "${{secrets.AZURE_AKS_SUBSCRIPTION}}"
-   azure-resource-group: the resource group where the cluster provisioned

    SAMPLE: 'rg-aks    
- cluster-name: Name of the cluster to target

    SAMPLE: aks-mycluster    
-   image-tag: the image tag to use in the helm chart

    SAMPLE: ${{github.sha}}
- cluster-namespace: the namespace to target

    SAMPLE: saga-nmp-poc    
- deployment-name: 'the name of the deployment "kubectl get deployments"'
    
    SAMPLE : saga-product-service

  

## Example 1
in this sample the values used for are fetched from the composite action azure-keyvault
    
     - uses: ./.github/actions/helm-upgrade
       with:          
        azure-credentials: ${{secrets.AZURE_CREDENTIALS_K8S}}
        chart-path: ${{env.helm-chart}}
        azure-subscription: ${{secrets.AZURE_AKS_SUBSCRIPTION}}
        azure-resource-group: ${{secrets.AZURE_AKS_RESOURCE_GROUP}}
        cluster-name: ${{env.cluster-name}}
        image-tag: ${{env.image-tag}}
        cluster-namespace: ${{env.namespace-prefix}}-dev
        deployment-name: ${{env.deployment-name}}

## Example 2

When referencing GitHub Actions (and composite) there are three main ways of creating a reference.

-  **account-name/repository-name/action-name@version-number**

-  **account-name/repository-name/action-name>@branch-name**

-  **account-name/repository-name/action-name@sha**

  

In the sample below we are using the sha (safest way) and the values are fetched from the azure-keyvault composite action

  
    - uses: accountname/repostory/helm-upgrade@<some-sha-value>    
       with:          
        azure-credentials: ${{secrets.AZURE_CREDENTIALS_K8S}}
        chart-path: ${{env.helm-chart}}
        azure-subscription: ${{secrets.AZURE_AKS_SUBSCRIPTION}}
        azure-resource-group: ${{secrets.AZURE_AKS_RESOURCE_GROUP}}
        cluster-name: ${{env.cluster-name}}
        image-tag: ${{env.image-tag}}
        cluster-namespace: ${{env.namespace-prefix}}-dev
        deployment-name: ${{env.deployment-name}}


