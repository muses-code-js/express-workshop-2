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

Now that we have `express` installed you probably want to get on with building our server.  But first lets talk briefly about what a server is.

A **server** is a computer program. Its job is to send and receive data.

A server "listens" on the network for requests sent to it from other programs that we call **clients**.  Depending on the request the server may perform some kind of work and then send some kind of response back to the client.  The request might be for some specific information that the server looks up in a database and then sends back as the response.  The response might just an error message like the famous *'Error 404: File not found.'*  

This idea of having client programs that make requests from server programs is called a **client/server architecture**.  It works because both the clients and the servers use the same format for the requests and responses.  This agreed upon format is called the **protocol**.

Our application is a web server.  The client is your web browser.  They use the `http` protocol to communicate.  The browser sends requests to the server using URLs to indicate what it wants from the server.

![Server flow](https://files.gitter.im/heron2014/FiiK/server.png)

But enough talk.  Let's code!

## Creating server.js

All of the code that we are going to write in this tutorial will go in one file,
`server.js`.  

We will now create that file and write the code to start the server running.

1. **Create a server.js file**

    Create a new file called `server.js`.  You can do this using the `File` menu in Cloud9.  Once created you will see it listed in the file view.  Double-click on it to open it in an editor.  It should be completely empty.

2. **Import the Express module**

    We already installed Express in Step 2, but we need a way to refer to it in our code so we can use it.  We do that using the function `require`.  

    To import Express, write the following at the top of `server.js`:

    ```javascript
var express = require('express');
    ```

    Now we have a variable `express` that points to whatever the Express module  exports.  We could have called this variable anything we wanted but it's common practice to use the same name.

3. **Create the server object**

    The Express module exports a single function.  When we **invoke** that function it returns an Express application object.  That object provides the all the behaviour that we use to build our server.

    Add the second line of code to your `server.js` file:

    ```javascript
var express = require('express');
var app = express();
    ```

    This new line invokes the `express()` from and stores the result in the variable `app`.

4. **Start our server "listening"**

    Now we have our server object (`app`) we can use its `listen()` function to start it listening for requests.

    The `listen()` function takes two arguments: a **port** number and a **callback function**.

    The **port number** can be thought of as a door number or apartment number.  Requests for this server will be sent "to that port". Every server running on the same computer must be listening on a different port.

    Cloud9 only allows you to use port `8080`.  If you are running Node.js on your own machine you can use any port between `1023` and `65535`.  We will use port `8080`.

    The **callback function** is a function for the server to run immediately after it starts listening.  We are going to use it to just display a message to let us known that the server started listening.

    Add the last three lines to `server.js`:

    ```javascript
    var express = require('express');
    var app = express();

    app.listen(8080, function () {
      console.log('Server has started listening on port 8080. ');
    });
    ```

## Start it up

You've built your server, but it isn't running yet.

To run a Node.js program we use the `node` program.

Type the following command in the Cloud9 terminal in the same directory as `server.js` and press ENTER:

```
node server.js
```

<!-- If you are using cloud9, you can also select the file `server.js` in the workspace folder tree and click the `Run` button on the top menu. -->

In the terminal you should see the following message displayed in your terminal:

![success](https://raw.githubusercontent.com/node-girls/workshop-cms/master/readme-images/step2-server02.png)

If you see this, congratulations! :clap: :clap: You have built yourself a server and started it running!
