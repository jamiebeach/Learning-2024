# [Exam AI-102: Designing and Implementing a Microsoft Azure AI Solution](https://learn.microsoft.com/en-us/credentials/certifications/exams/ai-102/)

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
- *As of Fall 2023, the Azure Personalizer Service is no longer available*
- An Azure AI service that uses **reinforcement learning** to empower your applications to make smarter decisions.
- Reinforcement learning is a process that enables Azure AI Personalizer to choose the best action for a given context, aiming to maximize a reward
- Rank and Reward APIs :
    - Rank : called when want to decision - return best action that maximizes total average reward.
    - Reward : Called to get feedback to help Azure AI Personalizer to learn whether Action ID it returned was vaulable.
- *Azure AI Personalizer learning loop*
- Can configure "exploration" to enable Azure AI Personalizer to find new patterns over time and adapt itself to users' behavioral changes.
- *Apprentice Mode* Azure AI Personalizer can begin its learning process by looking at the choices made by app's logic and mimic its decisions.
- *Inference explainability* helps better understand which features an action have that influence least or most.

## [Create computer vision solutions with Azure AI Vision](https://learn.microsoft.com/en-us/training/paths/create-computer-vision-solutions-azure-ai/)

### Analyze Images
- **Azure Vision Service** : designed to help you extract information from images. It provides functionality that you can use for :
    - Determining caption for an image
    - Detecting object
    - Detecting people
    - Determine metadata about image (size, color palette, clip art)
    - Identify appropriate category and if it contains known landmarks
    - Remove background
    - Determine if it contains adult or violent content
    - Read text in the image
    - Smart thumbnail generation

### Classify Images
- Azure AI Custom Vision
    - Use existing (labeled) images to train an Azure AI Custom Vision model.
    - Requires provisioning two resources:
        1. Training : An Azure AI Service or a Custom Vision (Training) Service
        2. Prediction : An Azure AI Service or a Custom Vision (Prediction) Service
    - To train :
        - Azure AI Custom Vision portal
        - Azure AI Custom Vision REST API or SDK
        - or a combination of both approaches

### Detect Objects in Images
- Use Azure AI Custom Vision service to create object detection models.
- Main difference from Classification model : Object detection detects bounding boxes of objects.
- There are two components to an object detection prediction:
    1. The class label of each object detected in the image.
    2. The location of each object within the image, indicated as coordinates of a bounding box that encloses the object.
- Requires provisioning two resources:
    1. Training : An Azure AI Service or a Custom Vision (Training) Service
    2. Prediction : An Azure AI Service or a Custom Vision (Prediction) Service
- Can use a single Azure AI Services resource for both training and prediction
- Can mix-and-match resource types (ex, use Azure AI Custom Vision (Training) resource to train a model, then publish using an Azure AI Services resource).
- The easiest option for labeling images for object detection is to use the interactive interface in the Azure AI Custom Vision portal.
- Subsequent labeling of new images can benefit from the smart labeler tool in the portal, which can suggest not only the regions, but the classes of object they contain.
- Alternatively : use a labeling tool, such as the one provided in Azure Machine Learning Studio or the Microsoft Visual Object Tagging Tool (VOTT),

### Faces : Detect, Analyze and Recognize
- Azure AI Vision Service : allows detection of people
- Azire Face API :
    - Face detection with bounding box
    - Feature analysis (pose, blur, glasses, landmarks, occlusion, etc)
    - Face comparison and verification
    - Facial recognition
- Face API Considerations :
    - Data privacy and security
    - Transparency
    - Fairness and inclusiveness
- Can do more than 1 person in an image.
- Can take video as input and detect 'livliness'
- Using identification, verification or recognition requires application to [limited access policy](https://aka.ms/cog-services-limited-access)
- Face ID's (guids) are cached by Azure for 24 hours. Can be used to compare with faces in other media
- Can train facial recognition on people's faces. In this case, face id is persisted.

### Azure Video Indexing
- Extract information from videos
- Can handle :
    - Facial recognition (requires Limited Access approval)
    - OCR
    - Speech transcription
    - Topic identification
    - Sentiment analysis
    - Label \\ tagging
    - Detection of adult or violent themes
    - Scene segmentation (break down video to scenes)
- Provides a portal to upload videos to and interactively view and analyze
- Video indexer can identify specific people in videos, if trained (requiring limited access approval)
- Can be trained to detect specific terminology that may not be in common usage
- Can be trained to recognize specific names of brands.
- Azure Video Indexer Widget is available to include Azure Video Indexer in your own custom HTML interfaces.
- REST API available to get information about account, including access token.
- ARM templates available

### Question and Answering Solution
- Use Azure AI Language to create a knowledge base of question and answer pairs (for supporting a chat bot or application)
- Azure AI Language includes a question answering capability - define a knowledge base of question and answer pairs that can be queried using natural language input.
- Can be published as a REST endpoint.
- Difference between Q&A and Language model is that the Q&A returns a static answer to a known question whereas the Language understanding returns its understanding to the intent of the question asked.
- Create a knowledge base:
    - write code that calls REST API\SDK to define, train and publish knowledge base. More common to use language studio.
    - Azure AI Services -> Language Service
    - Enable Q&A, Create or select Azure AI Search resource to host knowledge base index
    - In Language Studio, create a Custom Question Answering project
    - Add one or more data sources to populate knowledge base.
    - Edit question and answer pairs in portal
- Multi-turn conversations can be created (where there are follow-up questions and the like)
- Test and publish a knowledge base in Language Studio
- Then deploy to a REST endpoint.
- Consume from REST endpoint
- Active Learning can help you get better answer selection over time.
- 
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
