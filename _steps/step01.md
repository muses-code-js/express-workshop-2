---
layout: step
number: 1
title: Setting up your project
permalink: step01/

keywords:
  - term: package.json
    define: A `package.json` is the file used to store information about a Node.js project, such as its name and its dependencies. Read more [here](https://docs.npmjs.com/files/package.json).

  - term: dependencies
    define: Dependencies are external code modules that are required to run your project.

  - term: npm
    define: npm is a "package manager" for Node.js, meaning it allows you to easily install external modules (or chunks of code) published by others and use them in your project.

  - term: npm init
    define: The command used to create a new `package.json` file.  By default it will prompt the user for information, but using the `-y` flag will cause it to use the default values for each.

---

The first thing we do when starting a new Node.js project is create a `package.json` file.

`package.json` is the configuration file used by the program `npm`, the **Node Package Manager**.  It is used it configure lots of things in your project including module  depedencies, automating tasks, and how to publish it as a module.  

However the only thing we are going to use it for in this workshop is defining dependencies.

To create your new `package.json` file:

1. Open your terminal
2. Make sure you are in the `express-workshop-2` folder
3. Run the command `npm init -y`.

This creates a new file with default values and displays it for you.  

Your file will look something like:

```
{
  "name": "express-workshop-2",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/node-girls-australia/express-workshop-2.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/node-girls-australia/express-workshop-2/issues"
  },
  "homepage": "https://github.com/node-girls-australia/express-workshop-2#readme"
}
```

The syntax in this file is called **JSON** (pronounced like 'Jason') which is short for **Javascript Object Notation**. It's a way of representing Javascript data that is easy to read and write to and we use it a lot for saving and sending information.  We talk more about this in later steps.

Now we have a `package.json` file, let's add a dependency.
