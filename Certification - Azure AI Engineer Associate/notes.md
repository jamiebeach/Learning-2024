## [Get Started with Azure AI Services](https://learn.microsoft.com/en-us/training/paths/get-started-azure-ai/?ns-enrollment-type=Collection)

### Define Artificial Intelligence
- MS defines it with various types :
    - Vision
    - Text Analytics
    - Speech
    - Decision Making
 - AI Terms :
    - Data Science : focuses on processing of data; applying stats; exploring data
    - Machine Learning : training and validating predictive models
    - Artificial Intelligence : usually builds on machine learning to create sotware that emulates human intelligence 
- Considerations for Responsible AI
    - **Fairness** : AI systems should treat all people fairly.
    - **Reliability and Safety** : AI systems should perform reliably and safely
    - **Privacy and Security** : Should be secure and respect privacy.
    - **Inclusiveness** : Empower and engage people. Bring benefits to society.
    - **Transparency** : Be understandable and users made fully aware of system purposes and how it works.
    - **Accountability** : People should be accountable for AI systems.
 

### Authentication for Azure AI Services
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
## Running as Containers
- Azure AI services can be deployed as containers - either to AKS or even as a local container on-prem
- Numerous Speech, Language, Vision and Decision containers are available.
- When you deploy an Azure AI service container, must specify three items :
    - ApiKey : API key
    - Billing : service endpoint
    - Eula : "accept" that you accept the eula

## [Develop Decision Support Solutions with Azure AI Services](https://learn.microsoft.com/en-us/training/paths/develop-decision-support/)

### Azure Personalizer Service
- An Azure AI service that uses **reinforcement learning** to empower your applications to make smarter decisions.
- Reinforcement learning is a process that enables Azure AI Personalizer to choose the best action for a given context, aiming to maximize a reward
- Rank and Reward APIs :
    - Rank : called when want to decision - return best action that maximizes total average reward.
    - Reward : Called to get feedback to help Azure AI Personalizer to learn whether Action ID it returned was vaulable.
- *Azure AI Personalizer learning loop*
- Can configure "exploration" to enable Azure AI Personalizer to find new patterns over time and adapt itself to users' behavioral changes.
- *Apprentice Mode* Azure AI Personalizer can begin its learning process by looking at the choices made by app's logic and mimic its decisions.
- *Inference explainability* helps better understand which features an action have that influence least or most.


## [Machine Learning for Computer Vision](https://learn.microsoft.com/en-us/training/modules/analyze-images-computer-vision/2b-computer-vision-models)

- Convolutional Neural Networks (CNN): common ML architecture for computer vision
    - Use filters to extract numeric feature maps from images, and then feed the feature values into a deep learning model to generate a label prediction
    - CNNs have been core to computer vision for years
- Transformers
    - Foundational to modern LLMs
    - Work by processing huge volumes of data, and encoding language tokens (representing individual words or phrases) as vector-based embeddings (arrays of numeric values)
    - The embeddings are created such that tokens that are commonly used in the same context are closer together dimensionally than unrelated words.
 - Multi-modal models
   - Takes concept of transformers and NLP models and applies to images
   - Model is trained using a large volume of captioned images, with no fixed labels. An image encoder extracts features from images based on pixel values and combines them with text embeddings created by a language encoder. The overall model encapsulates relationships between natural language token embeddings and image features.
   - Microsoft Florence is an example of a multi-modal model. Is also a **foundation** model (a pre-trained general model on which you can build multiple adaptive models for specialist tasks).
