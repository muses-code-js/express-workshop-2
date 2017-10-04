---
layout: step
number: 3
title: Building the server
permalink: step03/

keywords:
  - term: server
    define: A web server is a software application which handles HTTP requests sent by the client, like web browsers, and returns web pages and information in response.

  - term: client
    define: A client requests services and information from the server. Typically, a client is a computer application, such as a web browser.

  - term: request
    define: A request is the message sent via HTTP from the client to the server, asking for information.

  - term: response
    define: A response is the data sent back to the client from the server after an HTTP request is made.

  - term: require()
    define: "`require()` is used in Node.js to import functionality from another file or an external module."

  - term: method
    define: Method is another name for a function.

  - term: port
    define: A port is a number that is used to identify each server running on a single machine.  Each running server on a machine must use it's own port number.  Port numbers start at 0 and go up to 65535.  The ports 0 to 1023 are reserved for specific services and require administrative permissions to use.

---


The first thing we need to do is build our server. You will always need to build a server when writing back-end code. A server can be built in pure Node.js, but Express gives us simpler syntax to work with.

## What is a server?

Servers are computer programs that receive requests from other programs, the *clients* and send back a response e.g share data, information or hardware and software resources.

### ...and what is a server in plain English?

A server is a computer program. Its job is to send and receive data.

Let's take a website for example.  A website is just a collection of HTML and CSS files, images, maybe some javascript files. When you type a website address in your browser's address bar, the browser (client) sends a **request** to the server that lives at that address. The browser asks the server to give it the files it needs to display the website properly.


![Server flow](https://files.gitter.im/heron2014/FiiK/server.png)

## 1. Create a `server.js` file

Let's build our server! Before we do anything, let's create a new file called `server.js`. This is where all our server code is going to live.

## 2. `require` the `express` library

We already installed Express in Step 2, but we need to make sure it is included in this file specifically so we can make use of its methods. In Node.js, when you want to access the functionality of a library or module in another file, you `require` it.

To import Express, write the following inside `server.js`:

```js
var express = require('express');
```

## 3. Initialise the server

To initialise our server, we just need to call the `express()` function. This will create an Express application for us to work with.

Add the second line of code to your `server.js` file:

```js
var express = require('express');
var app = express();
```

## 4. Start 'listening' for potential requests

One more step left, we need to set a **port** for our server to listen to. Think of a port as a door number; any requests that come to the server will come via that door. Setting a port will allow us to find where our server is running.

We use the **`app.listen`** method to do this. This method takes two arguments: a **port** and a **callback function** telling it what to do once the server is running. Need clarification? Read more about the `app.listen` method in the [Express documentation](http://expressjs.com/en/4x/api.html#app.listen).

We're going to run our server on port `3000` (`8080` if you are using cloud9), and run a simple `console.log` as our callback function. Update your `server.js` file, calling the `app.listen` method as follows:

if you are using a local environment:
```js
var express = require('express');
var app = express();

app.listen(3000, function () {
  console.log('Server is listening on port 3000. Ready to accept requests!');
});
```

And if you are using cloud9:
```js
var express = require('express');
var app = express();

app.listen(8080, function () {
  console.log('Server is listening on port 8080. Ready to accept requests!');
});
```

## 5. Switch the server on!

You've built your server, but it isn't running yet.

if you are using a local environment:

We need to run a command in the terminal to do this. We are going to use the `node` keyword to run the server file.

Type the following command in your terminal (or the cloud9 terminal):

```
$ node server.js
```

if you are using cloud9, you can also select the file `server.js` in the workspace folder tree and click the `Run` button on the top menu.


If you see this, congratulations! :clap: :clap: You have built yourself a server!

![success](https://raw.githubusercontent.com/node-girls/workshop-cms/master/readme-images/step2-server02.png)
