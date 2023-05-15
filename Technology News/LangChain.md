![[snapshots/NYSWn1ipbgg/00-00-12.png]]
# LangChain
![[snapshots/NYSWn1ipbgg/00-22-12.png]]
can create a personal assistant to answer questions about any YouTube video using LangChain. The video assistants that we're going to create will have four components which include model, memory, prompt and index. The models are the language models we will use and the memory is where the assistant stores the information it has received. Additionally, the prompt helps generate information, and we can use the index to manage our prompts. The agents can also be used to provide context-aware information. LangChain library will be used to develop the video assistants. So, in this video, we are going to walk through the core components and modules of LangChain and how they are used to create a video assistant app.## Overview
![[snapshots/NYSWn1ipbgg/00-11-03.png]]
This video is about how to create an AI application that can answer questions about a specific YouTube video using a large language model. The approach involves using document loaders, text splitters, and vector stores from the Lang chain library. 

![[snapshots/NYSWn1ipbgg/00-24-29.png]]
## Getting the Transcript
![[snapshots/NYSWn1ipbgg/00-15-38.png]]
To get the transcript of the video, we can use the YouTube loader from the document loaders and input the video URL.

![[snapshots/NYSWn1ipbgg/00-17-28.png]]
## Text Splitters
![[snapshots/NYSWn1ipbgg/00-18-00.png]]
Because the API of the large language model cannot handle a transcript with over 100,000 characters, the text splitter is used to split the document into chunks of 1,000 tokens each. 

![[snapshots/NYSWn1ipbgg/00-19-11.png]]
## Vector Databases
![[snapshots/NYSWn1ipbgg/00-19-28.png]]
Next, embeddings from open AI are used to convert the text splits into vectors, which will be used to create a vector [[database]] object. A similarity search is performed on this [[database]] to find pieces of information that are most relevant to the user's question.

![[snapshots/NYSWn1ipbgg/00-24-22.png]]
## Create DB and Get Response from Query
![[snapshots/NYSWn1ipbgg/00-20-46.png]]
The "create DB from YouTube video URL" function is used to create the [[database]], while the "get response from query" function is used to answer specific questions about the video transcript. The prompt and input messages are defined, and a similarity search is conducted on the [[database]] using the query provided.

![[snapshots/NYSWn1ipbgg/00-09-59.png]]
## Chaining Everything Together
![[snapshots/NYSWn1ipbgg/00-21-05.png]]
All of the functions are chained together using the chat and prompt models. The output not only returns the response, but also the documents used to obtain the answer.

![[snapshots/NYSWn1ipbgg/00-01-26.png]]
## Possibilities and Opportunities
![[snapshots/NYSWn1ipbgg/00-28-37.png]]
The possibilities for using this approach are endless. One suggestion is to create a list of channels that produce videos on a specific topic, and use the functions to extract useful information for research or social media content. Data Freelancer is recommended as a resource for those interested in freelance projects related to AI.

Source: [(142) Build Your Own Auto-GPT Apps with LangChain (Python Tutorial) - YouTube](https://www.youtube.com/watch?v=NYSWn1ipbgg)

