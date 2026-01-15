---
title: Understanding JSON
draft: false
tags:
---
Brief overview on JSON:
- javascript object notation 
- commonly used for apis and configs 

Json supported data types 
- strings
- numbers
- booleans
- null
- arrays
- objects - most used types - in a key value pairs

For example:
	`{`
	`"key":"value",`
	`"array":["si", "jsjs"],`
	`"objects": [{`
		`"so":"this si",`
		`"fav name":"kore"`
	`}]`
	`}`

	*PS: we donot put the comma in the last object key value pair* 


Now, let's understand more on how to deal with JSON on python 
- Python supports working with JSON through a built-in package called json. To use it, we import the json module in our Python script.
- JSON data is written as key-value pairs inside curly braces {}, which makes it very similar to Python dictionaries.

So, there are few of the things in which we can use the JSON to the max in python, they'll be : 
Reading or Writing or loading the data into some sort of file :

So, when we are reading a json file we simply:
### 1. Using json.load() 

The JSON package has ****json.load()**** function that loads the JSON content from a JSON file into a dictionary. It takes one parameter:

****File pointer:**** A file pointer that points to a JSON file.

****Example:**** Read a JSON file and convert its contents to a Python dictionary.

`import json`

#### `Read from file and parse JSON`
`with open("sample.json", "r") as f:`
    `data = json.load(f)`

`print(data)`
`print(type(data))`

here the load.json is the function that helps us to load the file

****Explanation:**** We open sample.json in read mode and use ****json.load()**** to parse its content into a Python dictionary, which we then print along with its data type.

### 2. Using json.loads()

****json.loads()**** function is used to parse a JSON string and convert it into a Python object. It takes one parameter:

****JSON string:**** A valid JSON-formatted string.

****Example:**** Convert a JSON-formatted string into a Python dictionary
`import json`
`json_str = '{"name": "hehe"}'`
`data = json.loads(json_str)`

`print(data)`
`print(type(data))`
****Explanation:**** We define a JSON string and use ****json.loads()**** to parse it into a Python dictionary, then print the resulting object and its type.

## Writing JSON to a file in Python

Writing data to a JSON file in Python involves converting Python objects like dictionaries into JSON format and saving them to a file. This process is called serialization. Let's explore two methods to write a JSON file in Python.

### 1. Using json.dumps() 

The JSON package in Python has a function called json.dumps() that helps in converting a dictionary to a JSON object. It takes two parameters:

- ****dictionary:**** the name of a dictionary which should be converted to a JSON object.
- ****indent:**** defines the number of units for indentation

After converting the dictionary to a JSON object, simply write it to a file using the "write" function.

****Example:**** Convert a dictionary to a JSON string and write it to a file.

`import json`
`data = {`
    `"name": "hhaha",`
    

`json_str = json.dumps(data, indent=4)`
`with open("sample.json", "w") as f:`
    `f.write(json_str)`

****Explanation:**** We create a dictionary, convert it to a JSON-formatted string using ****json.dumps()**** with 4-space indentation and write it to sample.json using the ****write()**** method.


## Python vs JSON Object Mapping

|PYTHON OBJECT|JSON OBJECT|
|---|---|
|Dict|object|
|list, tuple|array|
|str|string|
|int, long, float|numbers|
|True|true|
|False|false|
|None|null|
