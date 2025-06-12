---
title: part-2_module1
draft: false
tags:
  - complete
---
 
## Amazon Q Developer

Amazon Q Developer is designed for software developers, IT professionals, and data engineers. It integrates seamlessly into your development environment, whether in a code editor or through the command-line interface (CLI), helping you write, test, deploy, and maintain code more efficiently. Common use cases:

- **Code generation and testing**: Generate new code and make code upgrades and improvements, such as language updates, debugging, and optimizations.
    
- **Inline suggestions**: As you type commands, get real-time, context-aware suggestions to help complete tasks more efficiently.
    
- **Natural language chat**: Engage in conversations and ask questions in plain language, getting answers right within your terminal environment.
    
- **Debugging and troubleshooting**: Receive AI-driven suggestions to fix bugs and optimize code in real time.
    
- **Security scanning and fixes**: Automatically detect and address vulnerabilities in your code.
    

Amazon Q Developer helps speed up development processes, reduce errors, and improve code quality. It integrates with your existing workflows and tools, allowing you to enhance your work without disrupting the way you already build and deploy software.


Amazon Rekognition is one of the first purpose-built AI services that makes it easy to add image analysis to your application. With Amazon Rekognition, you can detect objects, scenes, and faces in images. You can also search and compare faces. Instead of just talking about it, let me open my AWS Management Console and show you Amazon Rekognition in action. It's such a fun service to use. Here in the console home, I can search for Rekognition with K,

then choose the option label detection. That's a little playground that Amazon Rekognition has, which provides you a sample image. You could upload your own image, but for this demo I'm just going to work with the default image around here. Amazon Rekognition tells me that there is a 98.7% chance

of having a person in these coordinates of the image, as well as a 98.1% chance of having a car in this image. And it's interesting, because you can upload things to Rekognition and Rekognition gives you back that information. This is the label detection. You can also navigate to image properties. So it tells you dominant colors, image moderation, facial analysis, and other types of image recognition as well. Although I interacted with the service via the AWS Management Console, you can also use Amazon Rekognition programmatically. In fact, most of the time you would want to do it programmatically. By programmatically, I mean from your script, application, or automation. Let me give you a real example of how you can use Rekognition in a homemade solution.



Amazon Comprehend is a purpose-built application. It has one goal and one goal alone, to analyze text. Lots and lots of text. I'm not kidding. That's what it does. Comprehend is a natural language processing service or NLP. This means that you're able to feed it a pile of text and it can scrape through it and categorize it for you. Now, what exactly does categorize mean?

Well, the first category is called entity recognition, meaning it can tell you who's referenced in the text. Where does this all take place? When does it take place? Basically, it'll pull out the key elements from the text and say, "Hey, these right here are important."

Now the next category is sentiment analysis. It can tell you if the text is generally positive, neutral, negative, or kind of mixed, so if you were to send it a collection of customer reviews for a product, it could understand that the statement, "This is the best app ever," is positive, while "I regret downloading this and will delete it immediately" is negative.

This is a helpful way to analyze collections of statements so you don't have to read each one and review it yourself. Next, it can identify key phrases so it'll know in the text where the important information is and where the not so important stuff is. It'll also figure out which language the text is written in, which can be helpful when you don't exactly know yourself.

It'll call out personally identifiable information or PII. When a customer accidentally sends you their credit card information in an email, yeah, Comprehend can pick it out of that text if you send it.



### Amazon Polly

Amazon Polly turns text into speech. It supports dozens of languages and voices and offers high-quality neural text-to-speech. This is especially useful for building applications that talk, narrate, or provide accessibility support.

Common use cases:

- Adding speech to apps and websites
    
- Narrating e-learning modules
    
- Providing audio accessibility features
    

### Amazon Lex

Amazon Lex helps you design, build, test, and deploy AI chatbots and voice assistants. You can integrate it with foundation and large language models to answer complex questions using data from your knowledge repositories.

Common use cases:

- Customer service bots
    
- Voice-enabled mobile or web apps
    
- Appointment and booking bots

## General-purpose AI and ML services

With general-purpose AI services, you can take full control over the ML lifecycle, including data preparation, model selection, training, testing, deployment, and monitoring. These tools are ideal for data scientists, ML engineers, and developers.

### Amazon SageMaker AI

Amazon SageMaker AI is a fully managed service for machine learning. With SageMaker, you can build, train, and deploy ML models quickly, without the need to manage your own servers. You can use built-in ML algorithms or bring your own models. SageMaker also includes a wide range of tools that support each step of the machine learning process. Some of the key features include:

- **Amazon SageMaker Studio**: A web-based interface where you can access everything you need to develop, train, and deploy models in one place.
    
- **Amazon SageMaker Data Wrangler**: Simplifies the process of preparing and transforming data, helping you move from raw data to training-ready datasets faster.
    
- **Amazon SageMaker Autopilot**: Automatically builds, trains, and tunes models based on your data, while still giving you control and visibility into the process.
    
- **Amazon SageMaker Clarify**: Identifies potential bias in your data and models and provides tools to improve transparency and fairness.
    
- **Amazon SageMaker Model Monitor**: Continuously checks your models in production to catch performance issues or data drift early.
    
- **Amazon SageMaker Debugger**: Offers real-time insights during training to help you understand model behavior and optimize performance.
    
- **Amazon SageMaker JumpStart**: Gives you access to pre-built models, example notebooks, and solutions so you can get started quickly with common use cases.
    

Common use cases:

- Building custom AI models to make predictions
    
- Detecting fraud or anomalies
    
- Creating recommendation engines
    
- Analyzing images or text for business-specific tasks