---
title: module 3
draft: false
tags:
  - complete
---
Amazon Bedrock:

With Amazon Bedrock, 
you can experiment with different pre-trained models, 
customize them for your needs, 
and integrate them into your generative AI applications. 

Fine-tuning trains the model on labeled examples. For example, let's say you are studying bird migration. You have thousands of labeled images of birds showing their species and whether they migrate in winter or not. You want AI to analyze new images and provide detailed descriptions. To do this, you'd need a multi-modal model, one that works with both; images and text. To start fine-tuning, you can store your labeled bird images in Amazon's Simple Storage Service, connect the dataset to your chosen model and let Bedrock do the rest. Bedrock will create a copy of your model, train it on your data, and give you a private version, fine-tuned to your needs. So when you upload a new bird image, the fine-tuned model will generate a much more accurate response than the original model code.


Unlike fine-tuning, continued pre-training doesn't require labeled data.

Instead, you feed the model large amounts of raw data such as thousands of bird photos. Over time, the model learns general patterns such as wing shapes, color variations, and other distinctive features. This helps the model improve its general understanding rather than learn specific facts.


 model distillation -- you can train a smaller model 
with the information from a large foundation model.
knowledge bases - These are private data sources that help the model improve accuracy and reduce hallucinations. To continue with the bird example, you could link your model to knowledge bases such as field guides and scientific papers. They would provide research-backed answers when you ask the model something specific to a bird industry or domain.


Amazon Q -- It is a generative AI assistant 
that transforms how work gets done, 
helping everyone to get insights on their data 
and accelerate their tasks. 
By using Amazon Q, you can streamline processes, 
get to decisions faster and be more productive.

As the name suggests, it is focused on software development tasks, but it's also useful for testing, deploying, troubleshooting, security scanning, modernizing applications, optimizing AWS resources, and creating data pipelines. This way, coders can get help with code related tasks, while data scientists can also get guidance to integrate AI/ML and enrich applications by adding generative AI capabilities


SageMaker will allow you to bring your own data, build your own machine learning models, and then predict your business's future, or at least make really educated guesses based on the data. Now, I could keep talking about SageMaker, but I'd rather show you how this works.


![[Pasted image 20250611073813.png]]



The Top P parameter determines what percentage of the most likely next word options the model considers when generating text. A lower Top P value means the model considers the words at the top of the list - the most likely or “safe” options. This makes the generated text more predictable and conservative. A higher Top P value means the model looks further down the list, considering some less likely or more “creative” word choices. This makes the output more diverse and unexpected, but also more prone to mistakes or nonsense.