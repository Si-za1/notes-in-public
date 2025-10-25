---
title: data cleaning and concepts
draft: false
tags:
  - complete
  - data
reference: datacamp tableau
---
 
**Data cleaning** is a foundational process in the data science lifecycle, and its role cannot be overemphasized when trying to uncover insights and generate reliable answers.

**Data quality** is the qualitative and or quantitative measure of how well our data suits the purpose it is required to serve. These measures are practical templates we can use to assess how suitable the data provided is for our desired purposes.

### Characteristics of quality data

1. **Accuracy**: A simple question we can ask to verify accuracy is - is the information contained in the data provisioned correctly in every detail? With data, we are trying to approximate patterns in the real world; accuracy helps define how true these approximations are.
   
2. **Relevance**: Is this information impactful to what our desired end goal is?
   
3. **Consistency**: Is the source of this data verified and can the information contained there be trusted? 
   
4. **Completeness**: Is the data provisioned and comprehensive enough for the desired end goal? 
   
5. **Uniformity**: Let's assume we have a sales column but not all transactions are made in the same currency. It becomes imperative to convert all the sales values into a single currency and that is what uniformity is about; ensuring that data measures are specified using the same units of measure in all systems.

### Data cleaning vs. data transformation

Data transformation is a set of processes that can help us extract more insights from the data provided. data transformation processes, the original representation of the data is altered. While it is still the same data, certain techniques have been introduced to transform it into a format usable for machine learning or some other purpose.

 - **Encoding:** This is a process of converting categorical values into binary values which can then be used in computations for machine learning.
 
  - **Data binning**: Also referred to as bucketing, this process helps to reduce the effect/size of minor observations. It entails grouping continuous values into bins (or categories).
  
 - **Scaling**: This is a common technique in machine learning to help standardize values of different scales into a fixed range.

## How Data Cleaning is Done

With the help of a set of guidelines to achieve high-quality data

The processes included in this workflow are:

- Data exploration
- Data cleaning
- Data verification
- Data cleaning reporting

### Data exploration

Data exploration is all about understanding the data via a deep exploration of the variables present in the data.
 Few points to be noted:
- #### Data Context

	- Before we can clean any data, we must understand the context of the data. Data context is the source of all entities contained in data.  This serves as a guiding light into what is acceptable in cleaning (and analysis)so we can derive the right insights from such data. 
	
	- Once we have a clear knowledge of how the data is/was collected, we then need to explore such data.

- **Exploratory data analysis** 
	- It refers to the critical process of performing initial investigations on data so as to discover patterns, spot anomalies, test hypotheses, and check assumptions with the help of summary statistics and graphical representations. 
	
> 	- _Data exploration is like walking into a crime scene as an investigative agent, where we passively observe all things out of place and data cleaning is the active process of solving the actual crime._

- There is no discovery without exploration. If we don't explore our data, it's difficult to discover the various issues existing within the data.

### Data cleaning
Once we uncover issues with our data using visual, aggregation, or statistical means, we need to fix them. **In this phase, data will either be removed, corrected, or imputed.**

#### Inconsistent Records
The best way to spot them can be via a frequency chart or making a distinct display of all values in the column. Some operations on inconsistent records will include but are not limited to:

- Converting strings to lower or proper case
- Removing white spaces
- Renaming column names

#### Data types and type conversion

The data type is simply how data is represented, which tells the compiler how the data is to be used.

### Missing data
This can be likened to a leaking roof and when it rains, it leaks.

There are two primary methods for dealing with missing data:

- Removal of data
- Imputation of data

Before any decision can be made on what method will be used, one must first examine the patterns of missing values across columns.

![[Pasted image 20251025133916.png]]

### Duplicates

We must ensure that we have a single source of truth for each observation. There are scenarios where we have multiple observations about a single customer, either because there is a double form submission by the user, or errors were made during data entry.

### Outliers

Outliers are extreme data points. They are usually very low or very high values that do not conform to the rest of the pattern in the data. Eg: - A customer who is 200 years of age.

**Identifying Outliers** There are different techniques to identify outliers either through visual means or statistical techniques

1. Sorting the dataset: By simply sorting the data, one can easily spot outliers within the dataset or variables of interest. However, this technique fails on large datasets and can be difficult to preview all values at a glance.
    
2. Visualization: Using Visual techniques such as boxplots, histograms and scatterplots can make it easy to detect outliers.
    
3. Using Z-scores: This is a statistical technique to quantify the unusualness of an observed value assuming the data follows a normal distribution. It is the number of standard deviations by which observed values fall above or below a mean value.
    

**Outlier Treatment Process** Outlier treatment serves as a process of removing or replacing outliers represented in our data:

1. **Remove outliers from the data:** This can involve removing values that lie at the lower or upper X_percentile of your data. The following are certain scenarios where outliers can be removed:
2. When it is obvious that the data is incorrectly measured. As mentioned earlier, an active customer who is 200 years is not a valid input, a typical example of an outlier that should be removed.
3. If the outlier doesn't change the results of your analysis, you may drop this outlier. This can also be considered when the number of outliers in the dataset is not much in comparison to the overall data.
    
4. **Replace outliers:** This involves replacing these extreme values with the mean, median or modal values. If the number of outliers is of considerable size in comparison to the actual data, then removing outliers will fail. **Note:** Mean values are susceptible to outliers. It is therefore advisable to consider the median or modal value for replacement.

## Data Verification

This is to verify the correctness and completeness of the data cleaning process, partly to ensure we didn't omit a step, and also to ensure we are in line with the data's context.

### Data cleaning, reporting, and automation

Reporting involves documenting the health of the data post-cleaning, as well as documenting the processes involved in the cleaning process.

[For hands-on](https://www.kaggle.com/learn/data-cleaning)

