---
title: part2-module3
draft: false
tags: []
---
 
# Data Foundations

When working with AI, it's important to understand the types and formats of data, the lifecycle it goes through, and why data quality matters in building AI solutions. At a high level, you’ll encounter two main types of data:

- **Labeled data**: This is data that comes with tags or annotations. For example, if you have a set of photos labeled “cat” or “dog,” that’s labeled data. Labeled data is necessary for supervised learning, where the model learns from examples.
- **Unlabeled data**: This is raw data without tags. It might be used for unsupervised learning or continued pre-training. Also, this type of data can be processed later with human input or automated labeling tools.

In terms of structure, data typically falls into these categories:

- **Structured data**: Organized into rows and columns, like a spreadsheet or database tables.
- **Unstructured data**: Free-form content such as emails, PDFs, social media posts, videos, or audio. This kind of data requires more preprocessing but is incredibly valuable for natural language and vision-based models.
- **Semi-structured data**: Falls somewhere in between structured and unstructured categories. As an example, think of JSON or XML files that aren’t rigidly formatted like tables, but they still have structure that can be parsed.

Additionally, there are other formats and types that play specific roles in AI:

|**Data Type**|**Description**|**Example Use Case**|
|---|---|---|
|Tabular|Rows and columns, like a CSV or SQL table|Forecasting sales|
|Time-series|Data indexed by time, often continuous|Monitoring sensors or stock trends|
|Text|Natural language documents, logs, or messages|Chatbots, document summarization|
|Image|Pixel-based files (JPEG, PNG)|Facial recognition, classification|
|Audio/Video|MP4 files, etc.|Speech recognition, object tracking|

Understanding these formats will help you choose the right tools, preprocessing methods, and model architectures later on.

## **The data lifecycle for AI solutions**

Creating a successful AI solution means understanding the full lifecycle of your data—from ingestion to deployment. Each phase builds on the previous, and skipping steps can lead to unreliable results.

Let’s walk through each stage and highlight the AWS services that can support you along the way.

**1. Data collection**: First, data needs to be ingested from internal or external sources. This could be an API, a file server, a database, or a real-time sensor feed. Some of the data collection tools include:

- Amazon Kinesis helps you collect streaming data. Kinesis also offers seamless integration and processing capabilities.
- AWS Database Migration Service (AWS DMS) helps you ingest data from relational databases. AWS DMS has configuration options and direct connections between on-premises and database services, such as Amazon Simple Storage Service (Amazon S3), that are hosted on AWS.
- AWS Glue is an extract, transform, and load (ETL) tool that helps you ingest unstructured data.

**2. Data preparation and cleaning**: Once collected, data often requires processing to be useful for training or analysis. This may include removing duplicates, filling in missing values, dropping irrelevant columns, masking sensitive data.

For transforming data, AWS offers several services:

- Amazon EMR: A big data platform that can run Apache Spark, Hive, or other frameworks for large-scale data transformations.
- AWS Lambda: Great for lightweight data processing or on-demand transformations.
- AWS Glue DataBrew: A visual, no-code tool for cleaning and transforming data, You can apply transformations, detect outliers, and preview results in real-time.
- Amazon SageMaker DataWrangler: Integrated with SageMaker Studio, it allows you to import, transform, and explore data from various sources.

**3. Quality checks**: Before moving forward, it’s essential to validate the quality of your data. This means checking for consistency, completeness, accuracy, and outliers. Here are some things to check:

- Completeness: Are any values missing? If so, how will you handle them?
- Consistency: Is the data uniform across sources and formats?
- Accuracy: Does it reflect reality, or are there errors in entry or labeling?
- Relevance: Is the data aligned with the task your model is trying to solve?
- Bias: Are certain groups underrepresented in your data?
- Timeliness: Is the data up to date?

AWS supports this through:

- AWS Glue DataBrew: Offers built-in data profiling features to spot missing values and anomalies.
- AWS Glue Data Quality: Allows you to define, monitor, and enforce data quality rules.
- Amazon SageMaker Clarify: Focused on fairness and bias detection. It helps evaluate the representation of different groups and explains model predictions.

**4. Visualization and analysis**: After data is cleaned and validated, you can begin exploring trends and patterns. This helps shape your AI approach. You can use tools like Amazon QuickSight to create dashboards and visualizations.

**5. Monitoring and debugging:** After the data is in production, you need to watch for drift, anomalies, or changes in format. This phase ensures that your model continues to perform well as new data arrives.

To detect the issues early:

- Amazon CloudWatch: Monitors infrastructure and application logs, helping detect anomalies and performance changes in real time.
- Amazon SageMaker Model Monitor: Monitors and analyzes models in production to detect data drift and deviations in model quality.

**6. Deployment and automation**: In AI systems, data often flows continuously into pipelines. Services like Amazon SageMaker Pipelines, AWS Lambda, and AWS Step Functions can automate steps in your workflow.

**7. Access control and governance**: Secure data access is essential. AWS Identity and Access Management (IAM) policies can help restrict who can view or modify sensitive datasets. This supports compliance and ensures responsible data use.

Strong data foundations are essential for reliable AI outcomes—whether you’re working with images, text, or tabular data, understanding data types, managing the data lifecycle, and evaluating data quality. With AWS tools and services, you can streamline these steps, but the goal remains the same: clean, well-prepared data is the key to effective AI.


---
How does data get into AWS?

The answer depends on your situation. If you have a large set of historical data, AWS Batch is a great way to bring it in. As the name suggests, this service processes data in batches. This prevents system overload and makes it easier to train AI on past trends. But what if you need to process data as it arrives in real time from sensory devices, social media, or websites? There is the Amazon Kinesis family of services that can capture and process data in real time and bring this data into a different service. Another approach is event-driven data collection. Amazon API Gateway and AWS Lambda can work together to collect and process data only when needed.

As you are bringing data into the cloud, what is next? Do you use it as is, or do you transform it before training your model?

But first, you need to understand what data you are working with. Is your data structured or unstructured? For fine-tuning, it's ideal to have labeled and well-organized examples. For continuous pre-training or training from scratch, raw data can still be useful.

Another key consideration is privacy. Does your data contain personally identifiable information? If so, you need to remove or mask it.

Finally, do you understand your data patterns? Knowing which fields are relevant for training or customization will help you get better results.

---

Imagine you are hired as a consultant cloud architect for a retail company that wants to automate the generation of product descriptions. Right now, they write descriptions manually, but they want a system that can generate text whenever they upload a new product image. What AWS services would you recommend? Let's compile a quick list.

We already discussed that Amazon Bedrock provides access to pre-trained foundation models, including large language models that specialize in text generation, so let's keep this service in mind.

Next, we need a way to analyze product images. Amazon Rekognition can help with that. Amazon Rekognition can detect objects, scenes, and concepts in images through DetectLabels API. After capturing labels, we can pass them to Amazon Bedrock to create a more accurate product description. But how do we get images into the cloud? Since the company isn't uploading large amounts of images constantly, we don't need a batch or streaming setup. Instead, we can use an event-driven workflow with Amazon API Gateway and AWS Lambda. Here is how the complete architecture works.

A client sends a request with a product image to Amazon API Gateway. For this to happen, you can set up a REST API in API Gateway. When API Gateway receives a request, it passes the request to AWS Lambda. Lambda needs to have a custom function and be configured with the appropriate roles and permissions to interact with both Amazon Rekognition and Amazon Bedrock. When Lambda receives a request, it calls Amazon Rekognition. Rekognition then uses machine learning to analyze the image and detect objects. Based on its analysis, it generates labels. Lambda takes these labels, creates a prompt, and sends the prompt to your large language model in Amazon Bedrock. Then the model can either enhance the existing basic description or generate a new description based on the detected objects. Additionally, you can configure parameters that control creativity and how long the description must be.

Finally, Lambda receives the generated text from Bedrock and returns it through API Gateway to the client.




![[Pasted image 20250613205246.png]]