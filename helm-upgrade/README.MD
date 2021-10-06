# Helm Upgrade 

  

## Purpose

the purpose of the composite action is to centralize the code that is used in a single file and avoid misconfiguration and duplicate code.

  

## How to use

  

if this composite action is placed in the repository it with the rest of the workflows see example 1.

if this repository is checked into a public repository see example 2.

  

## parameters

- **azure-credentials:**
    
    **Description:** ``credentials to login to Azure``

    **Required:** ``true``
    
    **Sample:**  ``${{secrets.AZURE_CREDENTIALS}}``
    
    
- **chart-path:** 

    **Description:** ``The path to the helm chart``

    **Required:** ``true``
    
    **Sample:** ``".helm/<my-chart>"``

    
- **azure-subscription:**
  
  **Description:** ``subscription where the cluster is provisioned``

    **Required:** ``true``
    
    **Sample:** ``"${{secrets.AZURE_AKS_SUBSCRIPTION}}"``
    
-   **azure-resource-group:** 
    
    **Description:** ``The resource group where the cluster provisioned``

    **Required:** ``true``
    
    **Sample:** ``rg-aks``
    
- **cluster-name:**

    **Description:** ``Name of the cluster to target``

    **Required:** ``true``
    
    **Sample:** ``aks-mycluster``
    
-   **image-tag:** 

    **Description:** ``the image tag to use in the helm chart``

    **Required:** ``true``
    
    **Sample:** ``${{github.sha}}``
    
- **cluster-namespace:**
    
    **Description:** ``The namespace to target``

    **Required:** ``true``
    
    **Sample:**  ``saga-nmp-poc``

- **deployment-name:**
    
    **Description:** ``The name of the deployment "kubectl get deployments"``

    **Required:** ``true``
    
    **Sample:** ``saga-product-service``
    

  

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


