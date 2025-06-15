---
title: amazon Q
draft: false
tags:
  - complete
---
 
# Amazon Q Developer integrations basics

# AWS Builder ID

Before installing and configuring Amazon Q Developer in your IDE and Amazon Q CLI in your Terminal, you are going to need an AWS Builder ID. *AWS Builder ID is a personal profile that provides access to select tools and services including Amazon CodeCatalyst, Amazon Q Developer, and AWS Training and Certification, it represents you as an individual and is independent from any credentials and data you may have in existing AWS accounts, it doesn’t need to be associated with an AWS Account, nor an IAM Entity.*

This is different from an AWS Account credential, and creating an AWS Builder ID is free. You only pay for the AWS resources you consume in your AWS accounts.

More information at: [https://docs.aws.amazon.com/signin/latest/userguide/sign-in-aws_builder_id.html](https://docs.aws.amazon.com/signin/latest/userguide/sign-in-aws_builder_id.html)

# Installing Amazon Q CLI and Amazon Q Developer in the IDE

## Amazon Q CLI

You can use Amazon Q Developer to enable completions for hundreds of popular CLIs like git, npm, docker, and aws. Amazon Q for command line integrates contexual information, providing Amazon Q with an enhanced understanding of your use case, enabling it to provide relevant and context-aware responses. As you begin typing, Amazon Q populates contextually relevant subcommands, options, and arguments.

In this webpage you can find download links for multiple Operating Systems: [https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-installing.html](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-installing.html)

After installing, you can log in with your AWS Builder ID, by typing q login, a modal window will open for authentication.

## Amazon Q Developer in the IDE

As of April 2nd, 2025, Amazon Q Developer is available in Visual Studio, Visual Studio Code (VS Code), Eclipse (preview) and the JetBrains family of integrated development environments (IDEs). Get started with Amazon Q in three steps:

**Install**

Install the Amazon Q extension for your editor (installation links below)

1. [JetBrains](https://plugins.jetbrains.com/plugin/24267-amazon-q) (IntelliJ IDEA and more)
    
2. [VS Code](https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.amazon-q-vscode)
    
3. [Eclipse (preview)](https://marketplace.eclipse.org/content/amazon-q)
    
4. [Visual Studio](https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.AWSToolkitforVisualStudio2022)
    

**Authenticate**

Authenticate with your Amazon Builder ID (instructions above)

**Develop software, chat inline, get suggestions, refactor, and transform.**

Amazon Q can be found in the activity bar in VS Code or the tool window anchored to the top-right space in IntelliJ IDEA.