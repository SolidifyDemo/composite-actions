# Get keyvault secrets from Azure

## Purpose

the purpose of the composite action is to centralize the code that is used in a single file and avoid misconfiguration and duplicate code.

  

## How to use

  

if this composite action is placed in the repository it with the rest of the workflows see example 1.

if this repository is checked into a public repository see example 2.

  

## parameters

- **azure-credentials**: 

    **Description:** ``the credentials used to login to Azure     ``
    
    **Required:** ``true``

    **Sample:**  ``${{AZURE_CREDENTIALS}}``

- **keyvault-name**: 

    **Description:** ``the name of the keyvault that secrets should be fetched from.``

    **Required:** ``true``
    
    **Sample:** ``mykeyvault``

- **keyvault-secrets:**

    **Description:**  ``A comma seperated string of secrets``

    **Required:** ``true``
    
    **Sample:** ``"secret1,secret2,secret3"``

  

## Example 1

    - uses: ./.github/actions/azure-keyvault
    with:
    azure-credentials: ${{secrets.AZURE_CREDENTIALS}}
    keyvault-name: 'keyvaultnmpdevelopment'
    keyvault-secrets: 'acr-server-url, acr-username, acr-password'
    id: keyvault

  

## Example 2

When referencing GitHub Actions (and composite) there are three main ways of creating a reference.

-  **account-name/repository-name/action-name@version-number**

-  **account-name/repository-name/action-name>@branch-name**

-  **account-name/repository-name/action-name@sha**

  

In the sample below we are using the sha (safest way)

  

    - uses: accountname/repostory/azure-keyvault@<some-sha-value>
       with:
    	   azure-credentials: ${{secrets.AZURE_CREDENTIALS}}
    	   keyvault-name: 'keyvaultnmpdevelopment'
    	   keyvault-secrets: 'acr-server-url, acr-username, acr-password'


  
  

## Access Secrets

To access the secrets from the composite action in your main pipeline use the

`` ${{env.<secret-name>}} ``

