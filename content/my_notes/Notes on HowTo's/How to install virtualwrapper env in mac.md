---
title: How to install virtualwrapper env in mac
draft: false
tags:
  - complete
---

To install `virtualenvwrapper` on your Mac using Zsh and create virtual environments for your projects, you can follow these steps:

### Step 1: Install `virtualenv` and `virtualenvwrapper`

1. Open your terminal (Zsh).
    
2. Install `virtualenv` using pip (if you haven’t already):
    
    ```bash
    pip install virtualenv
    ```
    
3. Install `virtualenvwrapper`:
    
    ```bash
    pip install virtualenvwrapper
    ```
    

### Step 2: Configure your Zsh shell

To make `virtualenvwrapper` available every time you open your terminal, you'll need to update your `.zshrc` configuration file.

1. Open the `.zshrc` file in your favorite text editor:
    
    ```bash
    nano ~/.zshrc
    ```
    
2. Add the following lines at the end of the `.zshrc` file to set up the `virtualenvwrapper` environment variables:
    
    ```bash
    # Virtualenvwrapper settings
    export WORKON_HOME=$HOME/.virtualenvs
    export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3
    source /usr/local/bin/virtualenvwrapper.sh #to actually find your source path 
    ```
    
    - `WORKON_HOME` is the directory where your virtual environments will be stored. The default is `$HOME/.virtualenvs`.
        
    - `VIRTUALENVWRAPPER_PYTHON` specifies which Python to use with `virtualenvwrapper` (make sure the path is correct; it might be different on your machine).
        
    - `source /usr/local/bin/virtualenvwrapper.sh` sources the script to make `virtualenvwrapper` commands available. 
    
     - To find your source path follow this:
     ```bash 
      find / -name "virtualenvwrapper.sh" 2>/dev/null
     ```

        
3. Save the file and exit (`Ctrl + X`, then `Y` to confirm).
    

### Step 3: Apply the changes

To make sure the changes take effect, reload the `.zshrc` file:

```bash
source ~/.zshrc
```

### Step 4: Create a Virtual Environment

Now you can create a virtual environment using `virtualenvwrapper`. For example:

```bash
mkvirtualenv myenv
```

This will create a new virtual environment named `myenv`. You can switch to it using:

```bash
workon myenv
```

### Step 5: Deactivate the Virtual Environment

When you’re done with the virtual environment, deactivate it:

```bash
deactivate
```


