## Bing Search
| API/Function | Description | API Examples |
| --- | --- | --- |
| Bing Autosuggest API | This API provides search suggestions while the user types, enhancing the search experience by offering possible queries based on the initial typed keywords. | `autosuggest(searchTerm)` |
| Bing Custom Autosuggest API | Allows developers to build a customized autosuggest feature for their applications, where suggestions are tailored to the specific content and scope of the service in question. | `customAutosuggest(searchTerm, customConfigId)` |
| Bing Custom Image Search API | Enables you to restrict image search results to specific domains or websites, providing a more focused and tailored set of images related to the search query. | `customImageSearch(searchTerm, customConfigId)` |
| Bing Custom Search API | Similar to custom image search but for web search results, this API lets you create a custom search experience over a defined set of webpages or domains. | `customWebSearch(searchTerm, customConfigId)` |
| Bing Custom Video Search API | Allows customization of video search results, filtering content from specific sources, domains, or across pre-defined content sets. | `customVideoSearch(searchTerm, customConfigId)` |
| Bing Entity Search | Provides detailed information about entities such as people, places, and things that can be found in a search query, offering a richer context and understanding of the topic. | `entitySearch(searchTerm)` |
| Bing Image Search API | Offers a straightforward image search experience, returning a comprehensive set of images related to the user's query. | `imageSearch(searchTerm)` |
| Bing News Search | Allows users to search for news articles on the web and retrieve results that include articles, images, and related news content. | `newsSearch(searchTerm)` |
| Bing Spell Check API | Offers a spell check service that considers context, grammar, and unusual words, providing corrections or suggestions for misspelled words within the text. | `spellCheck(text)` |
| Bing Video Search API | Searches the web for videos and returns a list of results, which may include thumbnails, snippets, and metadata for the videos. | `videoSearch(searchTerm)` |
| Bing Web Search | A comprehensive web search API that provides search results including webpages, images, videos, news, spell correction, and more. | `webSearch(searchTerm)` |



## Computer Vision

| API/Function | Description | API Examples |
| --- | --- | --- |
| Analyze Image | Extracts visual features based on image content, such as image description, categories, color scheme, and objects. | `analyzeImage(url, { visualFeatures, details, language })` |
| Analyze Image Domain | Recognizes and classifies domains in an image to apply domain-specific models such as celebrities or landmarks. | `analyzeImageByDomain(url, model)` |
| Analyze Image Domain In Stream | Analyzes an image stream for specific domains using domain-specific models. | `analyzeImageDomainInStream(imageStream, model)` |
| Analyze Image In Stream | Processes an image stream to extract information using various visual features. | `analyzeImageInStream(imageStream, { visualFeatures, details, language })` |
| Describe Image | Generates a description of an image in human-readable language with complete sentences. | `describeImage(url, { maxCandidates, language })` |
| Describe Image In Stream | Describes an image stream in natural language. | `describeImageInStream(imageStream, { maxCandidates, language })` |
| Detect Objects | Identifies objects within an image and provides location with bounding boxes. | `detectObjects(url)` |
| Detect Objects In Stream | Detects objects in an image stream and returns their locations. | `detectObjectsInStream(imageStream)` |
| Generate Thumbnail | Creates a thumbnail image from the original image, potentially applying smart cropping to focus on areas of interest. | `generateThumbnail(width, height, url, smartCropping)` |
| Generate Thumbnail In Stream | Generates a thumbnail from an image stream, with smart cropping. | `generateThumbnailInStream(width, height, imageStream, smartCropping)` |
| Get Area Of Interest | Identifies the area of interest in an image and crops it for focus. | `getAreaOfInterest(url)` |
| Get Area Of Interest In Stream | Determines the area of interest in an image stream and provides the coordinates for cropping. | `getAreaOfInterestInStream(imageStream)` |
| Get Read Result | Retrieves text recognition results from the Read operation, which extracts printed and handwritten text. | `getReadResult(operationId)` |
| List Models | Lists custom domain models trained within the service for various specialized recognitions. | `listModels()` |
| Read In Stream | Uses Optical Character Recognition (OCR) to extract printed text in various languages from an image stream. | `readInStream(imageStream, { language, detectOrientation })` |
| Recognize Printed Text | Recognizes printed text in an image and extracts words into machine-readable character streams. | `recognizePrintedText(url, { language, detectOrientation })` |
| Recognize Printed Text In Stream | Recognizes printed text in an image stream, allowing for the extraction of words into machine-readable text. | `recognizePrintedTextInStream(imageStream, { language, detectOrientation })` |
| Tag Image | Assigns tags to an image based on its content, facilitating image search and organization. | `tagImage(url, { language })` |
| Tag Image In Stream | Assigns tags to an image stream, aiding in categorization and retrieval. | `tagImageInStream(imageStream, { language })` |



## Face
| API/Function | Description | API Examples |
| --- | --- | --- |
| Face | Detects human faces in an image and returns face locations, landmarks, and optional attributes like head pose, age, and gender. | `detectWithUrl(imageUrl, returnFaceId, returnFaceLandmarks, returnFaceAttributes)`<br>`detectWithStream(imageStream, returnFaceId, returnFaceLandmarks, returnFaceAttributes)`<br>\/face\/v1.0\/findsimilars |
| Face List | Creates and manages a list of persisted face IDs for face identification. |POST {Endpoint}/face/v1.0/facelists/{faceListId}/persistedfaces |
| Large Face List | Manages large lists of faces for identification purposes. | `createLargeFaceList(largeFaceListId, name, userData)`<br>`deleteLargeFaceList(largeFaceListId)` |
| Large Person Group | Group faces for identification against a large dataset. | `createLargePersonGroup(largePersonGroupId, name, userData)`<br>`deleteLargePersonGroup(largePersonGroupId)` |
| Large Person Group Person | Manages people in large person groups. | `createPersonInLargePersonGroup(largePersonGroupId, name, userData)`<br>`deletePersonFromLargePersonGroup(largePersonGroupId, personId)` |
| Person Group | Group faces for identification against a smaller dataset. | `createPersonGroup(personGroupId, name, userData)`<br>`deletePersonGroup(personGroupId)` |
| Person Group Person | Manages people in person groups. | `createPersonInPersonGroup(personGroupId, name, userData)`<br>`deletePersonFromPersonGroup(personGroupId, personId)` |
| Snapshot | Take a snapshot of the face data for backup or for use in another region. | `takeSnapshot(snapshotType, objectId, applyScope)`<br>`getSnapshot(snapshotId)` |

## Language

| API/Function | Description | API Examples |
| --- | --- | --- |
| Conversation Analysis | Analyze conversation transcripts to gather insights. | POST {Endpoint}/language/:analyze-conversations?api-version=2023-04-01 |
| Conversation Analysis Runtime | Run real-time analysis on live conversations. |  |
| Conversational Analysis Authoring | Create and manage models for conversational analysis. | Numerous APIs available |
| Question Answering | Build a Q&A system for your data to easily manage and query. | `POST /language/query-knowledgebases`\nParameters: `projectName`, `deploymentName`, `knowledgebaseName`, and in the request body: `{"question": "your question"}` |
| Question Answering Projects | Manage projects for setting up a question answering system. | Project management in Azure's QnA Maker or Language Service involves using the Azure portal or specific APIs for creating, updating, and deleting knowledge bases, but direct API calls like `manageQAProjects` are not specified. |
| Text Analysis Authoring | Build models for analyzing text to understand sentiment, extract key phrases, and more. | For custom text analysis, Azure provides the Text Analytics Client Library, where you can use methods like `client.analyzeSentiment(documents)`, `client.extractKeyPhrases(documents)` but does not directly offer an "Authoring" endpoint. |
| Text Analysis Runtime | Execute text analysis models in real-time. | Direct API calls for runtime text analysis include endpoints like `/text/analytics/v3.1/sentiment` for sentiment analysis, `/text/analytics/v3.1/entities/recognition/general` for entity recognition, with request bodies containing the text to be analyzed. |