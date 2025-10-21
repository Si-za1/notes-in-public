---
title: Medical Terms | Clinical aspects
draft: false
tags:
  - in-progress
---
- **About the MIMIC - III dataset de-identification**
    
    Before data was incorporated into the MIMIC-III database, it was first deidentified in accordance with Health Insurance Portability and Accountability Act (HIPAA) standards using structured data cleansing and date shifting. The deidentification process for structured data required the removal of all eighteen of the identifying data elements listed in HIPAA, including fields such as patient name, telephone number, address, and dates. In particular, dates were shifted into the future by a random offset for each individual patient in a consistent manner to preserve intervals, resulting in stays which occur sometime between the years 2100 and 2200. Time of day, day of the week, and approximate seasonality were conserved during date shifting. Dates of birth for patients aged over 89 were shifted to obscure their true age and comply with HIPAA regulations: these patients appear in the database with ages of over 300 years.
    
    Protected health information was removed from free text fields, such as diagnostic reports and physician notes, using a rigorously evaluated deidentification system based on extensive dictionary look-ups and pattern-matching with regular expressions[6](https://www.nature.com/articles/sdata201635#ref-CR6). The components of this deidentification system are continually expanded as new data is acquired.
    
- **SOAP notes**
    
    SOAP notes are **a method for documenting patient encounters, with each letter standing for a section: Subjective, Objective, Assessment, and Plan**. They are used by healthcare providers to systematically record information about a patient's condition, allowing for clear and concise communication, consistent documentation, and effective treatment planning.
    
    **S: Subjective**
    
    - This section includes information reported by the patient, such as their feelings, concerns, and their own description of their symptoms.
    - It can also include the client's goals and perceptions of their problems.
    
    **O: Objective**
    
    - This contains factual, observable, and quantifiable data gathered by the healthcare provider.
    - Examples include vital signs, physical examination findings, test results, and observations of the patient's appearance and behavior.
    
    **A: Assessment**
    
    - This is the healthcare provider's professional judgment and analysis of the patient's condition.
    - It combines the information from the Subjective and Objective sections to determine a diagnosis or potential problem areas.
    
    **P: Plan**
    
    - This outlines the next steps for the patient's care.
    - It includes recommendations for treatment, management, and any necessary follow-up appointments
- **HIPPA**
    
    [https://www.hhs.gov/hipaa/for-professionals/special-topics/de-identification/index.html](https://www.hhs.gov/hipaa/for-professionals/special-topics/de-identification/index.html)
    
- **ICU and ACU**
    
    🏥 **ICU – Intensive Care Unit**
    
    ---
    
    **What it is:**
    
    The ICU is a **specialized hospital unit** where **critically ill or unstable patients** receive **continuous monitoring and advanced life support** (like mechanical ventilation, IV drips, or dialysis).
    
    **Examples of ICU patients:**
    
    - A person recovering from major surgery
    - Someone with sepsis or organ failure
    - A patient on a ventilator after a heart attack
    
    **In EHR datasets (like MIMIC-III):**
    
    - ICU data is very detailed and high-frequency.
    - It includes **vitals recorded minute-by-minute**, **lab results**, **medication administration logs**, and **clinical notes**.
    - That’s why the **MIMIC-III** dataset is famous — it comes from the ICU of the Beth Israel Deaconess Medical Center in Boston and provides rich, time-stamped health data for research.
    
    **Important note:**
    
    Because ICU patients are extremely ill, results from ICU datasets **don’t always generalize** to the general hospital population — which is why the paper mentions the need for external validation.
    
    ---
    
    ### 🩺 **ACU – Acute Care Unit (or Acute Medical Unit)**
    
    **What it is:**
    
    An **Acute Care Unit (ACU)** is for patients who need **urgent but not critical** care — in between a general ward and the ICU.
    
    **In simple terms:**
    
    - ICU → life-threatening or unstable conditions
    - ACU → serious but stable conditions (need close observation, not intensive life support)
    
    **Example ACU patients:**
    
    - Someone with pneumonia needing oxygen but not a ventilator
    - A patient with diabetic complications needing IV fluids and monitoring
    - Post-surgery patients recovering before transfer to a general ward
    
    ---
    
    ### ⚖️ ICU vs. ACU comparison
    
    |Feature|ICU|ACU|
    |---|---|---|
    |**Patient condition**|Critical, unstable|Serious, but relatively stable|
    |**Monitoring**|Continuous, minute-to-minute|Regular, but frequent|
    |**Staff ratio**|High (1 nurse per patient)|Lower (1 nurse for several patients)|
    |**Data richness (EHR)**|Extremely detailed|Moderate detail|
    |**Common in datasets like MIMIC-III**|✅ Yes|❌ Usually not (MIMIC focuses on ICU only)|
    
    ---
