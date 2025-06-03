---
title: affirmation_generator
draft: false
tags:
  - complete
---

# **Affirmation Generator – Study Note**

### 📌 Goal:

Build a command-line tool that generates a short, themed affirmation quote using the OpenAI API based on the genre selected by the user.

---

## GitHub Repository

📎 **Source Code:** [👉 _GitHub repo link here_](https://github.com/Si-za1/python_for_beginners/blob/30daysai/30daysAI/day1.py)

---

## Core Components

|Function|Description|
|---|---|
|`user_choice_genre()`|Asks user to choose a genre and keeps prompting until a valid one is selected|
|`affirm_generation(user_choice)`|Uses OpenAI API to generate a quote based on the selected genre|
|`main` block|Orchestrates the flow: user input → quote generation → output display|

---

## Genres Available

```python
["motivational", "inspirational", "emotional"]
```

---

## 🐞 Errors Faced & Fixes

### 1. **UnboundLocalError: cannot access local variable 'user_choice'**

- **Problem:** `user_choice` was referenced in the `while` loop before being defined. 
    
- **Solution:** Defined `user_choice = input(...)`  inside the function itself so that it won't be unbound.
    

---

### 2. **Input Prompt Appeared Twice**

- **Problem:** `user_choice_genre()` was called **twice**, leading to two prompts. 
    
- **Solution:** Stored the return value of the function in a variable and reused it in the second function calling with affirm_generation().
    

---

### 3. **Only One Retry Allowed for Invalid Genre**

- **Problem:** Used `if` instead of a `while` loop for input validation.
    
- **Solution:** Replaced `if` with `while` so the user is re-prompted until valid input is entered.

---
### 4. **Error: `'in <string>' requires string as left operand, not list`**

- **Cause:** 
    
    `while genres not in user_choice:`
    
    Here, `genres` is a **list**, but `in` expects the **left operand to be a string** when checking membership in another string.
    
- **Fix:** Reverse the check to:
    
    `while user_choice not in genres:`
    
    Now, it's checking if the string `user_choice` is inside the list `genres`, which is correct.
--- 
