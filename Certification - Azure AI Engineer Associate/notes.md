# [Exam AI-102: Designing and Implementing a Microsoft Azure AI Solution](https://learn.microsoft.com/en-us/credentials/certifications/exams/ai-102/)

[![Azure AI-102 Mindmap](../images/azure-ai-mindmap.svg)](../images/azure-ai-mindmap.svg)

## [Azure Cognitive Serivces API Reference](https://learn.microsoft.com/en-us/rest/api/cognitiveservices/?view=rest-cognitiveservices-translator-v3.0)

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
- [Custom vision website](https://www.customvision.ai/)
- Custom Vision Service lets you export your classifiers to run offline. You can embed your exported classifier into an application and run it locally on a device for real-time classification.
- Custom Vision Service only exports projects with compact domains. The models generated by compact domains are optimized for the constraints of real-time classification on mobile devices. Classifiers built with a compact domain may be slightly less accurate than a standard domain with the same amount of training data.
- [How to run the exported custom vision model with Python](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/export-model-python)

### Detect Objects in Images
- Use Azure AI Custom Vision service to create object detection models.
- Main difference from Classification model : Object detection detects bounding boxes of objects.
- There are two components to an object detection prediction:
    1. The class label of each object detected in the image.
    2. The location of each object within the image, indicated as coordinates of a bounding box that encloses the object.
- Requires provisioning  resources:
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

### [Machine Learning for Computer Vision](https://learn.microsoft.com/en-us/training/modules/analyze-images-computer-vision/2b-computer-vision-models)

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

### Explore Azure AI Services for Vision (preview)
- Microsoft's Florence large foundation model - significant improvements to image analysis and groundbreaking customization capabilities
- Using updated Image Analysis 4.0 service, devs can use the Azure Computer Vision APIs to quickly and easily integrate image analysis functionality into applications.
- Features :
  - Create image captions
  - Human readable descriptions
  - Extract and read text
  - Detect faces
  - Search visual inputs using natural language queries
- Provides low-code UI-based tool for trying the capabilities
- **Florence Foundation Model**
    - trained on billions of text-image pairs
    - able to recognize things from a small number of sample photos (few-shot)
    - Previously, required minimum of 15 images. Now can be as few as 4 images.
    - **Caption** generates a single sentence describing image, evaluating image content hollistically
    - **Dense Captions** provides supplementary information, generating descriptive phrases for individual objects in the image.
    - **Image Retrieval** in Image Analysis 4.0 - vectorization converts incoming queries to vectors and matches images based on semantic closeness. Search images using natural language.
    - **Tagging** identify content within an image (objects, actions, living beings, scenery)
    - **Object Detection** similar to tagging but API returns tag plus bounding box coords for each object found.
    - **OCR** provides fast sync api for scenarios that include single images without text-heavy - near real-time.
    - People detection, background removal, smart image thumbnails (all like previous iteration of Vision Service.
- Vision Studio :
    - Azure Computer Vision's newest tool, provides unified portal experience for Image Analysis 4.0.
    - **Spatial Analysis** : video summary, frame locator, count people in an area, detect position of people.
- Can train the models when pre-trained models may not be accurate enough.
    - Training images must be stored in an Azure Storage Account container to be accessible by the model.
- COCO file : 
    - Common Object in Context (COCO) - JSON files used for storing information about training images and associated annotations.
- Dataset and Model objects

## [Develop Natural Language Processing with Azure AI](https://learn.microsoft.com/en-us/training/paths/develop-language-solutions-azure-ai/)
### Analyze Text
- Azure AI Language detection API
    - documents must be less than 5120 characters
    - and api calls must be less than 1000 items
    - Each item contains an id and the text to be analyzed
    - Response includes predicted language and confidence level 0 to 1
    - Mixed language content within the same document returns the language with the largest representation in the content, but with a lower positive rating
- Extract key phrases
    - Key phrase extraction works best for larger documents (the maximum size that can be analyzed is 5,120 characters).
    - As with language detection, the REST interface enables you to submit one or more documents for analysis.
- Sentiment Analysis
    - Overall document sentiment is based on sentences:
        - If all sentences are neutral, the overall sentiment is neutral.
        - If sentence classifications include only positive and neutral, the overall sentiment is positive.
        - If the sentence classifications include only negative and neutral, the overall sentiment is negative.
        - If the sentence classifications include positive and negative, the overall sentiment is mixed.
- Extract Entities
- Extract Linked entities

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

### Build a Conversational Language Understanding Model
- NLP (Natural Language Processing) vs NLU (Natural Language Understanding) - determining semantic meaning from natural language
- User Input -> NLU Model determines meaning -> App performs action
- [Azure AI Language Documentation](https://learn.microsoft.com/en-us/azure/ai-services/language-service/overview)
- Pre-configured features
    - Summarization : summarizes text into key sentences; available for both documents and conversations
    - Named entity recognition : extract and identify entities (people, places, companies)
    - Personally Identifiable Information (PII) detection : identify, categorize and redact PII
    - Key Phrase Extraction
    - Sentiment Analysis
    - Language Detection
- Learned features : requires labeling data, training and eploying model to make available.
    - Conversational Language Understanding (CLU) : helps users build custom natural language understanding models to predict overall intent and extract important information
    - Custom named entity recognition : use custom labeled data to extract specified entities from unstructured text.
    - Custom text classification
    - Question answering
- [Language Studio](https://language.cognitive.azure.com/)
- Can also use REST API to build model
- Authentication : must provide following header in each API call to authentiate :
```
Ocp-Apim-Subscription-Key="The key to your resource"
```
- Can query the model via SDK or REST API
- **Utterances** : phrases that a user might enter
- **Intent** : represents a task or action the user wants to perform (ie. meaning of utterance)
- [Supported pre-built entities](https://learn.microsoft.com/en-us/azure/ai-services/language-service/conversational-language-understanding/prebuilt-component-reference)
- Add phrase : AddPhraseListAsync(appId, versionId, new PhraselistCreateObject(...))
- To run via docker : 
    - docker run command. docker run --rm -it -p 5000:5000 --memory 8g --cpus 1 mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment Eula=accept Billing={ENDPOINT_URI} ApiKey={API_KEY}

### [Create a custom text classification solution](https://learn.microsoft.com/en-us/training/modules/custom-text-classification/)
- Part of NLP is the ability to classify text. Azure provides 
- Types of classification projects :
    - **Single label classification**
    - **Multiple label classification**
- False positive - model predicts x, but the file isn't labeled x.
- False negative - model doesn't predict label x, but the file in fact is labeled x.
- **Recall** - Of all the actual labels, how many were identified; the ratio of true positives to all that was labeled. Measures the model's ability to predict actual positive classes. It's the ratio between the predicted true positives and what was actually tagged. The recall metric reveals how many of the predicted classes are correct.
Recall = #True_Positive / (#True_Positive + #False_Negatives)
- **Precision** - How many of the predicted labels are correct; the ratio of true positives to all identified positives. Measures how precise/accurate your model is. It's the ratio between the correctly identified positives (true positives) and all identified positives. The precision metric reveals how many of the predicted classes are correctly labeled.
Precision = #True_Positive / (#True_Positive + #False_Positive)
- **F1 Score** - A function of recall and precision, intended to provide a single score to maximize for a balance of each component 
- [Azure AI Evaluation Metrics](https://learn.microsoft.com/en-us/azure/ai-services/language-service/custom-text-classification/concepts/evaluation-metrics?azure-portal=true)
- Custom Classification Workflow :
- ![custom classification flow](https://learn.microsoft.com/en-us/training/wwl-data-ai/custom-text-classification/media/classify-development-lifecycle-small.png)
- Split datasets for training : **Training dataset** and **Testing dataset**
    - Random or manual splitting
- Most usage of REST API for Azure AI Language service is asynchronous (get results using URI returned in original request header)  

### Create a custom named entity extraction solution
- Custom named entity recognition (NER)
- Extract people, place, thing from documents
- Has built-in NER
    - [Full list of things recognized here](https://learn.microsoft.com/en-us/azure/ai-services/language-service/named-entity-recognition/concepts/named-entity-categories?azure-portal=true&tabs=ga-api).
- The Azure AI Language service enforces the following restrictions:
    - Training - at least 10 files, and not more than 100,000
    - Deployments - 10 deployment names per project
    - APIs
    - Authoring - this API creates a project, trains, and deploys your model. Limited to 10 POST and 100 GET per minute
    - Analyze - this API does the work of actually extracting the entities; it requests a task and retrieves the results. Limited to 20 GET or POST
    - Projects - only 1 storage account per project, 500 projects per resource, and 50 trained models per project
    - Entities - each entity can be up to 500 characters. You can have up to 200 entity types.
- Language Studio is the easiest way to label data
- The confusion matrix allows you to visually identify where to add data to improve your model's performance.

### Translate text with Azure AI Translator service
- API for translating text between 90 supported languages
- Capabilities :
    - Language detection.
    - One-to-many translation.
    - Script transliteration (converting text from its native script to an alternative script).
- Language Detection :
    - Detect endpoint
- Translation
- Transliteration :
    - translate to different script. Ex : Japanese to latin script
- Translation options :
    - Word alignment
    - Sentence length
    - Profanity filtering (no action, marks, deleted)
- Custom translations :
    -  you can create a custom model that maps your own sets of source and target terms for translation
    - assigns new category that you can use as parameter
    
### Azure AI Speech
- Speech to text
    - Speech to text API, which is the primary way to perform speech recognition.
    - Speech to text Short Auido API, optimized for short streams of audio (60 seconds)
- Text to speech
    - Text to speech API, which is the primary way to perform speech synthesis.
    - Batch synthesis API, which is designed to support batch operations that convert large volumes of text to audio
    - Can configure audio format and voices
        - standard voices
        - neutral voices
    - Speech synthesis markup language (SSML). XML based syntax offers greater control over how the spoken output sounds.
- Speech translation
    - Similar to speech recognition, with addition of source and target languages
    - TranslationRecognizer returns translated transcriptions of spoken input - essentially translating audible speech to text.
    - Can synthesize the translated speech in one of 2 ways :
        - Event-based : Set voice in TranslationConfig; Create event handler in TranslationRecognizer Synthesizing event; use Result.getAudio() method. Can only use when translating to single target language.
        - Manual : Use TranslationRecognizer to get translated text; use a SpeechSynthesizer to synthesize voice. 
- Speaker recognition
- Intent recognition
- Direct Line Speech : end-to-end solution for creating a flexible, extensible voice assistant. It's powered by the Bot Framework and its Direct Line Speech channel, that is optimized for voice-in, voice-out interaction with bots.
    - Could create a voice assistant bot with this.
- Access to Speech resources can be managed by RBAC. Speech resource needs a custom subdomain and use a private endpoint.


## [Knowledge Mining and Cognitive Search](https://learn.microsoft.com/en-us/training/paths/implement-knowledge-mining-azure-cognitive-search/)

### [Azure AI Search](https://learn.microsoft.com/en-us/training/modules/create-azure-cognitive-search-solution/)
- Azure AI Search provides a cloud-based solution for indexing and querying a wide range of data sources, and creating comprehensive and high-scale search solutions.
    - Index documents
    - Enrich index data
    - Extract insights for analysis
- **Replicas** : instance of the search service. Can increase speed\resiliency. 
- **Partitions** : divide index into multiple storage locations - allows for splititng I/O operations.
- Number of search units = number of replicas * number of partitions. (R*P=SU)
- Supports multiple data source types : 
    - Unstructured files in blog storage container
    - Tables in Azure SQL Database
    - Documents in CosmosDB
- Apps can also push data directly into the index with JSON
- Can apply AI (skills) as part of indexing process
- The indexer is the engine that drives the overall indexing process.
- Outputs from each skill can be used as inputs into following skills
- Full text search - Lucene query syntax
    - Lucene : Simple vs Full
- Query processing consists of four stages:
    1. Query Parsing
    2. Lexical analysis
    3. Document retrieval
    4. Scoring
- Query filters : 
    - Include filter criteria in a simple search expression.. OR
    - Provide OData filter expression as $filter
- Facets : a useful way to present users with filtering criteria based on field values in a result set
    - To use facets, you must specify facetable fields
- Sorting results : by default : relevance
- Search as you type
    - Retrieval 
    - Autocomplete
- Custom scoring : by default, search results sorted by relevance. Calculated based on a term-frequency/inverse-document-frequency (TF/IDF) algorithm.
- Synonym Maps
- Parallel indexing : If you partition your data, you can create multiple indexer-data-source combinations that pull from each data source and write to the same search index. Because each indexer is distinct, you can run them at the same time, populating a search index more quickly than if you ran them sequentially : https://learn.microsoft.com/en-us/azure/search/search-howto-large-index#run-indexers-in-parallel

### [Knwoledge Mining with Cognitive Search](https://learn.microsoft.com/en-us/training/paths/implement-knowledge-mining-azure-cognitive-search/)
- Implement custom skills as web-hosted services (such as Azure Functions) that support the required interface.
- Must impement expected schema: JSON structure; input and output schemas.
- Custom.WebApiSkill skill type
- Skill definition : 
    - Specifies API endpoint URI
    - Set context re: which point in document hierarchy skill can be called
    - Assign input values
    - Store output in new field

### [Create a knowledge store with AI Search](https://www.deeplearningbook.org/)
- Azure AI Search enables defining a knowledge store in the skillset that encapsulates your enrichment pipeline.
- The knowledge store consists of projections of the enriched data, which can be JSON objects, tables, or image files.
- When an indexer runs the pipeline to create or update an index, the projections are generated and persisted in the knowledge store.
- **Projections** : projections of data to be stored in your knowledge store are based on the document structures generated by the enrichment pipeline in your indexing process.
- Shaper Skill : creates a well-formed JSON document, easier to map to a projection in a knowledge store than the more complex document that has been built iteratively by the previous skills in the enrichment pipeline.

## [Enrich a Search Index with Language Studio](https://ai102srch887224144.search.windows.net)
- Language Studio groups its features into the following areas:
    - Classify text
    - Understand questions and conversational language
    - Extract information
    - Summarize text
    - Translate text
- Features can be either preconfigured or customizable. Preconfigured features can be tested straight away with a demo-like environment directly inside Language Studio. You can use them straight out of the box.
- The other features with * and green cogs in their logo need user customization. They require you to train their models so they fit your data better.
- Conversational language understanding aims to build a model that predicts intention from conversational text. For example, imagine an email app that you can chat with to send email messages or flag emails.
- The most flexible way to create a Language Studio project is to first create your language service using the Azure portal. If you choose this option, you get the option to add custom features.
- be default it will use 80% of the documents to train the model and 20% to blind test it

### [Knowledge Mining with Cognitive Search](https://learn.microsoft.com/en-us/training/paths/implement-knowledge-mining-azure-cognitive-search/)
- Azure Cognitive Search implements an enhanced version of Apache Lucene for full text search.
- Stages of Query Processing : 
    - Query Parsing
    - Lexical Analysis
    - Document retrieval
    - Scoring
- You can tell the search explorer to use the Lucene Query parser by adding &queryType=full to the query string.
- Lucene syntax, you can write more precise queries.
- Can boost search terms : Category:luxury^3
- Azure Cognitive Search uses the BM25 similarity ranking algorithm. The algorithm scores documents based on the search terms used.
- The search engine scores the documents returned from the first three phases. The score is a function of the number of times identified search terms appear in a document, the document's size, and the rarity of each of the terms. 
- By default search results are ordered by their search score
- Cognitive Search lets you influence a document score using scoring profiles.
- The scoring profile can also include functions, for example, distance or freshness. Functions provide more control than simple weighting, for example, you can define the boosting duration applied to newer documents before they score the same as older documents.
- You can add up to 100 scoring profiles to a search index.
- Functions can be used in scoring profile - magnitude, freshness, distance, tag
- If you don't specify an analyzer for a field, the default lucene analycer is used.
- Microsoft provieds 50 analyzers across different languages
- Specialized analyzers exist too - language-agnostic. (ex : patternAnalyzer)
- A custom analyzer consists of: 
    - Character filters. These filters process a string before it reaches the tokenizer.
    - Tokenizers. These components divide the text into tokens to be added to the index.
    - Token filters. These filters remove or modify the tokens emitted by the tokenizer.
- The tokenizer is the component that divides the text into the tokens that will be stored in the index. 
- 13 different tokenizers to choose from.
- After tokenization can apply token filtering. 41 filters available.
- Analyze Text with REST api - submit text and ensure tokens returned properly.

### [Search Data Outside of Azure](https://learn.microsoft.com/en-us/training/modules/search-data-outside-azure-platform-cognitive-search/02-index-data-from-external-data-sources-factory)
- Push data from external data sources using Azure Data Factory
    - zero code option
    - index needs to be created first (ADF can't create indexes yet)
- Azure Cognitive Search Push API
    - Most flexible way to push data into Cognitive Search
    - Batch documents in the request up to 1000 documents or 16 MB total in size

### [Maintain an Azure Cognitive Search Solution](https://learn.microsoft.com/en-us/training/modules/maintain-azure-cognitive-search-solution/01-introduction?ns-enrollment-type=learningpath&ns-enrollment-id=learn.wwl.implement-knowledge-mining-azure-cognitive-search)
- Secure ACS by focusing on :
    - Inbound search requests made by users to your search solution
    - Outbound requests from your search solution to other servers to index documents
    - Restricting access at the document level per user search request
- Encrypts data with service managed keys
- Can use Azure Key Vault
    - an advantage of using your own keys with AKV is that double encryption will be enabled on all objects you use custom keys on.
- Use firewall to restrict ingress
- Harden with expressroute, azure gateway and app service
- Default auth is key based. Admin and Query keys
- Can use RBAC 
    - Grant roles to administrator
    - Define roles for querying
- Can restrict which documents a user can search using search.in filter
- Measure performance with diagnostics settings
    - select alllogs and allmetrics and send to log analytics
- How your search queries perform is directly connected to the size and complexity of your indexes. The smaller and more optimized your indexes, the fast Azure Cognitive Search can respond to queries.
- Can scale out your index for performance. Up to 12 partitions.
- MAke highly available
    - 2 replicas guarantee 99.9% for queries
    - 3 or more replicas guarantee 99.9% for both querynig and indexing
    - Use availability zones (at least standard tier)
- Azure Monitor
- Write Kusto queries against ACS logs
- Customer-managed keys require an additional billable service, Azure Key Vault, which can be in a different region, but under the same subscription, as Azure Cognitive Search.
- Enabling Customer-managed keys (CMK) encryption will increase index size and degrade query performance.

### [Implement knowledge mining with Azure Cognitive Search](https://learn.microsoft.com/en-us/training/paths/implement-knowledge-mining-azure-cognitive-search/)
- **Semantic Search** : Semantic search is a capability within Azure Cognitive Search that aims to improve the ranking of search results. Semantic search improves the ranking of search results by using language understanding to more accurately match the context of the original query.
- 2 functions :
    1. Improves ranking
    2. Improves query results with captions and answers
- Semantic ranking : [BM25 ranking](https://learn.microsoft.com/en-us/azure/search/index-similarity-and-scoring)
- Semantic ranking 
    - takes the top 50 results from the BM25 ranking results.
    - The results are split into multiple fields as defined by a semantic configuration. 
    - The fields are converted into text strings and trimmed to 256 unique tokens.
    - Strings are passed to machine reading comprehension models to find the phrases and sentences matching query.
    - Results of this summarization phrase is a semantic caption and, optionally, a semantic answer.
    - The semantic captions are now ranked based on the semantic relevance of the caption.
    - The results are then returned in descending order of relevance.
- Advantages : 
    - Results more closely match query semantics
    - Can render an answer
- You enable semantic search at the service level and, once it is enabled, semantic search is available for all indexes. Semantic search cannot be enabled or disabled on a per-index basis.

### [Improve search results using vector search in Azure Cognitive Search](https://learn.microsoft.com/en-us/training/modules/improve-search-results-vector-search/)
- Vector search is a new capability available in Cognitive Search used to index, store and retrieve [**vector embedding**](https://dev.to/_madfrog/vector-embedding-101-the-key-to-semantic-search-kmd) from a search index. You can use it to power applications implementing the [**Retrieval Augmented Generation (RAG)**](https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview) architecture, similarity and multi-modal searches or recommendation engines.

![vector query](https://learn.microsoft.com/en-us/training/wwl-data-ai/improve-search-results-vector-search/media/vector-search-architecture-diagram.png)

- A vector query can be used to match criteria across different types of source data by providing a mathematical representation of the content generated by machine learning models.
- Use cases :
    - LLM
    - Similarity search (multi-modal)
    - Represent and find documents in any language
    - Filters to reduce data that vector search needs to process
- Customer managed keys aren't supported
- There are storage limitations
- You need to encode your Azure Cognitive Search query by sending it to an embedded model. The response is then passed to a search engine to complete a search over the vector fields.

### Embeddings
-An embedding is type of data representation that is used by machine learning models. An embedding represents the semantic meaning of a piece of text. You can visualize an embedding as an array of numbers, and the numerical distance between two embeddings represents their semantic similarity. For example, if two texts are similar, then their representations should also be similar.
- Embedding space is the core of vector queries comprising all the vector fields from the same embedding model. It comprises of all the vector fields populated using the same model.


## [Develop solutions with Azure AI Document Intelligence](https://learn.microsoft.com/en-us/training/paths/extract-data-from-forms-document-intelligence/)

### [Plan an Azure AI Document Intelligence solution](https://learn.microsoft.com/en-us/training/modules/plan-form-recognizer-solution/)

- **Azure AI Document Intelligence** is an Azure service that you can use to analyze forms completed by your customers, partners, employers, or others and extract the data that they contain.
- Use a model to inform Azure AI Document Intelligence about the type of data you expect to be in the documents you're analyzing
- Azure AI Document Intelligence outputs data in JSON format
- Several pre-built models : 
    - General document analysis :
        - Read
        - General document
        - Layout
    - Others expect specific forms :
        - Invoice
        - Receipt
        - W-2 US Tax declaration
        - ID DOcument
        - Business card
        - Health insurance card
- Composed model : multiple custom models trained on different types of documents associated into single model.
- Built on Azure AI Vision
- Use Azure AI Visino with OCR for extracting simple words from photos. Use Azure AI DOcument Intelligence for more complicated documents.
- Azure AI Document Intelligence Studio

### [Use prebuilt Azure AI Document Intelligence models](https://learn.microsoft.com/en-us/training/modules/use-prebuilt-form-recognizer-models/)

- If you want to use Document Intelligence to extract data from a common forms or documents, you can choose to use a prebuilt model and you don't have to train your own.
- You must also comply with these requirements when you submit a form for analysis:
    - The file must be in JPEG, PNG, BMP, TIFF, or PDF format. Additionally, the Read model can accept Microsoft Office files.
    - The file must be smaller that 500 MB for the standard tier, and 4 MB for the free tier.
    - Images must have dimensions between 50 x 50 pixels and 10,000 x 10,000 pixels.
    - PDF documents must have dimensions less than 17 x 17 inches or A3 paper size.
    - PDF documents must not be protected with a password.
- Use api endpoint and api key (from portal) to call via REST API
- Takes several seconds to respond, so best to call asynchronously.
    - StartAnalyzeDocumentFromUriAsync()
    - WaitForCompletionAsync()
- If you want to extract text, languages, and other information from documents with unpredictable structures, you can use the read, general document, or layout models.
- Read : read model extracts printed and handwritten text from documents and images
    - TheIdeal if you want to extract words and lines from documents with no fixed or predictable structure.
- General : extends read. Can identify entities such as people, organizations, dates.
- layout model returns selection marks and tables from the input image or PDF file
- Invoice model
- Receipt model
- ID document model
- business card model
- W-2 model

### [Extract data from forms with Azure Document Intelligence](https://learn.microsoft.com/en-us/training/modules/work-form-recognizer/)
- Azure Document Intelligence is a Vision API that extracts key-value pairs and table data from form documents.

### [Create a composed Form Recognizer model](https://learn.microsoft.com/en-us/training/modules/create-composed-form-recognizer-model/)
- Composed models in Azure AI Document Intelligence enable users to submit a form when they don't know which is the best model to use.
- You can create custom models of two types:
    - **Custom template models** - consistent visual template. 
    - **Custom neural models** - for when forms are less consistent, semi-structured or unstructured.
- Can do 100's of custom models in single Azure AI Document Intelligence resource
    - Depends on tier. Standard tier has many times more.
- Once you have created a set of custom models, can assemble them into a composed model.
    - Can use Azure AI Document Studio
- Composed model has a modelid
- Individual models in composed model can be identified with doctype in returned json
- Format must be JPG, PNG, PDF (text or scanned), or TIFF. Text-embedded PDFs are best because there's no possibility of error in character extraction and location.
- File size must be less than 50 MB.


### [Build an Azure AI Document Intelligence custom skill for Azure Cognitive Search](https://learn.microsoft.com/en-us/training/modules/build-form-recognizer-custom-skill-for-azure-cognitive-search/)

- If you integrate Cognitive Search with an Azure AI Document Intelligence solution, you can enrich your index with fields that your Azure AI Document Intelligence models are trained to extract.
- Use document intelligence for custom skillset for indexing


## [Develop Generative AI solutions with Azure OpenAI Service](https://learn.microsoft.com/en-us/training/paths/develop-ai-solutions-azure-openai/)

### [Get started with Azure OpenAI Service](https://learn.microsoft.com/en-us/training/modules/get-started-openai/)
- currently in limited access
- **Azure OpenAI Studio**
- Types of generative AI models :
    - GPT-4
    - GPT-3.5
    - Embeddings
    - DALL-E
- For chat based models, use chat completions for api calls
- Azure OpenAI Studio has a playground (looks similar to OpenAI playground)
- **Temperature** : controls randomness. Higher = more random\creative
- **Max Length** : limits number of tokens per response. 4000 max. Token is about 4 characters.
- **Stop Sequences** : Make responses stop at a desired point such as end of sentence.
- **Top Probabilities** : Like temperature. Controls randomness. Higher = more random.
- **Frequency Penalty** : Reduce chance of repeating token.
- **Presence Penalty** : Reduce chance of repeating token.
- **Pre-Response Text** : Insert text after input and before model's response. Can help prepare the response.
- **Post-Response Text** : Insert text after the model's response to encourage further input.

### [Build natural language solutions with Azure OpenAI Service](https://learn.microsoft.com/en-us/training/modules/build-language-solution-azure-openai/)
- Endpoints :
    - Completion - model takes an input prompt, and generates one or more predicted completions
    - ChatCompletion - model takes input in the form of a chat conversation (where roles are specified with the message they send), and the next chat completion is generated
    - Embeddings - model takes input and returns a vector representation of that input