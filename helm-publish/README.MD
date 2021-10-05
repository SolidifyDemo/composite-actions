# Publish Helm Chart 

  

## Purpose

the purpose of the composite action is to centralize the code that is used in a single file and avoid misconfiguration and duplicate code.

  

## How to use

  

if this composite action is placed in the repository it with the rest of the workflows see example 1.

if this repository is checked into a public repository see example 2.

  

## parameters
- chart-path: the path to the helm chart

    SAMPLE:  ".helm/<my-chart>"
    
- helm-registry-url: The full url to the remote registry

    SAMPLE: "https://myacr.azurecr.io"    
- helm-registry-username: The username to authenticate to the external registry
    
    SAMPLE: "my-user"

- helm-registry-password: The username to authenticate to the external registry
    
    SAMPLE: "my pass" (should always be secret)
  

## Example 1
in this sample the values used for are fetched from the composite action azure-keyvault

    - uses: ./.github/actions/helm-publish
      with:          
        helm-registry-url: ${{env.acr-server-url}}
        helm-registry-username: ${{env.acr-username}}
        helm-registry-password: ${{env.acr-password}}
        chart-path: ${{env.helm-chart}}

## Example 2

When referencing GitHub Actions (and composite) there are three main ways of creating a reference.

-  **account-name/repository-name/action-name@version-number**

-  **account-name/repository-name/action-name>@branch-name**

-  **account-name/repository-name/action-name@sha**

  

In the sample below we are using the sha (safest way) and the values are fetched from the azure-keyvault composite action

  
    - uses: accountname/repostory//helm-publish@<some-sha-value>
      with:          
        helm-registry-url: ${{env.acr-server-url}}
        helm-registry-username: ${{env.acr-username}}
        helm-registry-password: ${{env.acr-password}}
        chart-path: ${{env.helm-chart}}



