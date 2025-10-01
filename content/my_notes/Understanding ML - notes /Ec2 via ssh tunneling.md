---
title: Untitled
draft: false
tags:
  - complete
---
# A Journey from EC2 to S3

Starting a self-project on cloud infrastructure is an intense learning experience. This post details my journey setting up an end-to-end Machine Learning environment using AWS, specifically an EC2 instance for compute and S3 for storage. I cover the setup process, the real-world errors I faced, how I solved them, and the steps taken to train my first simple model.

## Phase 1: Setting Up the Infrastructure

The project goal was simple: host a Jupyter Notebook on a free-tier **EC2 instance** (`t2.micro`), store data in **S3**, and train a **scikit-learn model**.

1. **S3 Bucket Creation:** I created a bucket (e.g., `siza-ml-project-data`) and immediately focused on a **clean structure** by creating a `raw-data/` folder to upload the Iris dataset.
    
2. **EC2 Launch:** I launched the EC2 instance, focusing on the **Security Group** to open ports:
    
    - **Port 22 (SSH):** For terminal access.
        
    - **Port 8181 (Custom):** For the Jupyter Lab/Notebook interface (I later used SSH tunneling to map this locally).
        

## Phase 2: The Troubleshooting Journey 🛠️

My biggest hurdle wasn't the code; it was establishing a reliable connection. I used **VS Code's Remote-SSH extension** to connect, which led to a series of permission and configuration errors.

|Error Message|Cause of Error|Solution Taken|
|---|---|---|
|**"Failed to parse remote port from server output"**|The minimal Linux AMI lacked essential build tools needed for the VS Code Remote Server component to install correctly.|**Installed dependencies** on the EC2 instance via basic SSH.|
|**"keyword identityfile extra arguments..."**|Syntax error in the `~/.ssh/config` file. I used a backslash (`\`) to escape spaces in the key path, which SSH Config doesn't accept.|**Wrapped the key path in quotes** in the config file: `IdentityFile "~/downloads/backup documents/newpair.pem"`.|
|**"Load key: Operation not permitted"**|**File permissions** issue on my **local machine** (macOS). The key was in a cloud-synced folder, which often restricts access for security reasons.|**Moved the key** to the secure `~/.ssh/` directory and set the strict permissions: `chmod 400 ~/.ssh/newpair.pem`.|
|**"Permission denied (publickey...)"**|This was a final catch-all error after fixing the above. The likely cause was an **incorrect username** for the AMI (e.g., trying to use `ec2-user` on an Ubuntu image).|**Verified the AMI's default user** (e.g., changing `User ec2-user` to `User ubuntu` in the SSH config).|

By addressing these issues, I finally established a stable, secure connection and launched my Jupyter Lab environment within VS Code.

## Phase 3: Data Loading and Model Training

With the EC2 environment ready, the focus shifted to the core task: connecting to S3 and training a model.

### 1. Data Loading from S3

Instead of manually uploading, I used **`boto3`** (the AWS SDK for Python) to programmatically pull the data from S3, which is the standard cloud workflow.

- **Action:** Installed `boto3` on the EC2 instance.
    
- **Code:** Used the `s3.download_file()` method to pull the `Iris.csv` from my `raw-data/` folder in S3 to the EC2's local directory for processing.
    

### 2. Model Training: The 7-Step Approach

I adopted a structured 7-step data science process for the Iris dataset:

1. **Project Planning & Data Acquisition:** Iris dataset.
    
2. **Data Cleaning/Preparation:** Verified no missing values (`df.isnull().sum()`).
    
3. **Exploratory Data Analysis (EDA):** Used `df.describe()` and **Seaborn's `pairplot`** to visually inspect feature relationships and confirm clear separation between the _Setosa_ species and the others.
    
4. **Feature Engineering:** Not needed for this simple dataset.
    
5. **Model Training:** Split the data (70/30) and trained a **K-Nearest Neighbors (KNN)** classifier.
    
6. **Evaluation:** Achieved high accuracy on the test set, confirming the model's performance.
    

## Phase 4: Next Steps [ Still need planning !!]

The initial project is complete, but the learning continues. My next steps are focused on productionizing the model and further leveraging AWS services:

1. **Model Persistence:** Ensure the final model and prediction results are uploaded back to S3 using `boto3.upload_file()`. This keeps my project outputs safe and separate from the compute environment.
    
2. **Cost Management:** Set up AWS Budgets and alarms to monitor EC2 usage and prevent unexpected charges, staying safely within the Free Tier.
    
3. **Infrastructure Clean-up:** Practice good cloud hygiene by **terminating the EC2 instance** when not in use.
    
4. **Next Project:** Tackle a more complex, larger dataset (like the Kaggle House Prices dataset) that will require **data preprocessing (scaling, encoding)** and a different model (e.g., Scikit-learn's `LinearRegression` or `RandomForest`). This will necessitate using the EC2 instance's computational power more extensively.