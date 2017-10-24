---
layout: step
number: 7
title: Saving New Posts (1/4)
permalink: step07/

keywords:
  - term: GET
    define: An HTTP method for fetching data. Read more [here](http://www.w3schools.com/tags/ref_httpmethods.asp). For more detailed docs [read this](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)
  - term: POST
    define: An HTTP method for sending data. Read more [here](http://www.w3schools.com/tags/ref_httpmethods.asp). For more detailed docs [read this](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)
  - term: middleware
    define: Functions in Express that run before the final request handler.  A nice article explains in more depth [here](https://www.safaribooksonline.com/blog/2014/03/10/express-js-middleware-demystified)
  - term: express-formidable
    define: An Express middleware function that parses (reads) form and file data from the request.  Documentation on it [here](https://www.npmjs.com/package/express-formidable)

---

Now that we can display our posts, the next part is creating new ones.

How this is expected to work is that we will type something into the textbox in the page, click "POST" and your content will be saved on the server and displayed in the page.  

Much like the previous step, in order to make that work we will have to implement the appropriate endpoint with the behaviour that the page expects.

This endpoint has the following requirements:

1. Endpoint URL: `/create-post`
2. Request Method: `POST`

However this behaviour is relatively complicated compared to the previous one:

1. Post content will be sent as form field `blogpost`
2. New post is to be added to existing posts in `posts.json` using current timestamp as its property name & saved to disk
3. New post entry should be sent back as response.

There's quite a bit to cover here, so we are going to split this one up over a four steps.  For the first one, we will just create the endpoint and extract our content.

## The /create-post endpoint

So far all of the endpoints you have created have been for the `GET` request method because you have been requesting data from the server.  However this time you will be sending new data to the server for it to save so we will use the `POST` request method.  

Add the following to `server.js`:

```javascript
app.post('/create-post', function(request, response){

});
```

## Extracting our post

Your new post content from the text box is sent in the request as "form data".  This makes it difficult to extract.  However someone has written a nice package called `express-formidable` for extracting form data.

Install `express-formidable` using NPM with this command.  This is exactly the same as when you installed `express`.

```
npm install express-formidable --save
```

Once it is installed import at the top of `server.js` using `require`.  

```javascript
var formidable = require('express-formidable');
```

This time we didn't use exactly the same name as the package.  This is because you can't use `-` in a variable name.

`express-formidable` is a middleware function, like `express.static()`.  So we have to tell our `app` object to use it.

Add the following line to `server.js` after your `app.use(express.static())` line and before your endpoints.

```javascript
app.use(formidable());
```

Sometimes the order that middlware functions are added with `app.use()` is important.  This depends on the middleware functions you are using. In this case, `express-formidable` must be added *after* `express.static()`.  

What `express-formidable` does is automatically extract form data from the request, and add it back as an easy to use object called `fields`.

To verify that it is working, add a `console.log` statement to your **handler function** to log this object.

```javascript
app.post('/create-post', function(request, response){
  console.log(request.fields);
});
```

Test this by:

1. Make sure `server.js` is saved.
2. Stop and start the server again.
3. Go to the app in your browser, type something in the box and click POST.

In your terminal you should see your post logged:

[INSERT SCREENSHOT]

If it isn't working for you, you can double-check that your code is right with the solution below:

```javascript
var express = require('express');
var formidable = require('express-formidable');
var fs = require('fs');

var app = express();

app.use(express.static('public'));
app.use(formidable());

app.post('/create-post', function(request, response){
  console.log(request.fields);
});

app.get('/get-posts', function(request, response){
  fs.readFile(__dirname+'/data/posts.json', function(error, data){
    if(error){
      console.log('Error reading posts.json: '+error);
      response.status(500);
      response.send(error);
    } else {
      response.send(data);
    }
  });
});

app.listen(8080, function () {
  console.log('Server has started listening on port 8080. ');
});
```
{: .solution }
