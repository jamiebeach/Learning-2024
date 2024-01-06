## [Get Started with Azure AI Services](https://learn.microsoft.com/en-us/training/paths/get-started-azure-ai/?ns-enrollment-type=Collection)

Authentication for Azure AI Services
- By default, restricted by subscription keys
- Should protect keys with Azure Key Vault
- Some AI services may require a token. Auth token can be retrieved with subscription id and is then valid for 10 minutes.
- Support for Microsoft Entra ID authentication and service principals
    - Code :

    ```
    Set-AzContext -SubscriptionName <Your-Subscription-Name>
    $account = New-AzCognitiveServicesAccount -ResourceGroupName <your-resource-group-name> -name <your-account-name> -Type <your-account-type> -SkuName <your-sku-type> -Location <your-region> -CustomSubdomainName <your-unique-subdomain-name>

    $SecureStringPassword = ConvertTo-SecureString -String <your-password> -AsPlainText -Force
    
    $app = New-AzureADApplication -DisplayName <your-app-display-name> -IdentifierUris <your-app-uris> -PasswordCredentials $SecureStringPassword
    
    New-AzADServicePrincipal -ApplicationId <app-id>
    
    New-AzRoleAssignment -ObjectId <your-service-principal-object-id> -Scope <account-id> -RoleDefinitionName "Cognitive Services User"
    ```
- Managed identities : 2 types
    - System-assigned
    - User-assigned
    ```
    az vm identity assign -g <my-resource-group> -n <my-vm>
    ```
