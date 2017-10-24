---
layout: step
number: 8
title: Saving New Posts (2/4)
permalink: step08/
keywords:
  - term: Date
    define: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date
#  - term: JSON
#    define: A format for storing and transporting data. Read more [here](http://www.w3schools.com/js/js_json.asp). Or for more detailed docs [read this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
#  - term: fs
#    define: A core Node.js module for interacting with the file system on your computer.  Read more [here](https://nodejs.org/dist/latest-v4.x/docs/api/fs.html#fs_file_system)
#  - term: fs.readFile()
#    define: Asynchronously reads the entire contents of a file
#  - term: fs.writeFile()
#    define: Asynchronously writes data to a file

---

Ok we've got our form data.  The next thing we need to do is construct the object that will hold that data.  This is the object that we will be adding to our saved data and that we will be sending back as the response.

The frontend expects the `/create-post` endpoint to send back the object that we will be adding to our `posts.json` file.

## Making a new post object

Our blog post objects have two fields: `timestamp` and `content`.

**timestamp** is a number that tells us the exact time that the post was made.  It's actually the number of milliseconds since 1 January 1970 (UTC).  We can get this value using the function `Date.now()`.

**content** is the post that was sent.  We get that from `request.fields.blogpost`.

We use both of those values to put together a new object which we call `newPost`.

Update your `/create-post` route like below:

```javascript
app.post('/create-post', function(request, response){
  var now = Date.now();

  var newPost = {
    timestamp: now,
    content: request.fields.blogpost
  }

});
```

## Sending the new post object back

Now that we have our new post object we have to send it back in the response.  

We do that with `response.send()`.

Update your `/create-post` route like below:

```javascript
app.post('/create-post', function(request, response){
  var now = Date.now();

  var newPost = {
    timestamp: now,
    content: request.fields.blogpost
  }
  response.send(newPost);

});
```

The frontend expects the response to contain the object converted into a JSON string.  `response.send()` automatically does that conversion for you if you pass it an object.  

## Test it out

Restart your server again and try to create some new posts.  

You should see your new posts added to the page.

[INSERT SCREENSHOT]

But remember that we haven't actually saved the new post yet so if you refresh the page they all disappear.  

If it isn't working for you, you can double-check that your code is right with the solution below:

```javascript
var express = require('express');
var formidable = require('express-formidable');
var fs = require('fs');

var app = express();

app.use(express.static('public'));
app.use(formidable());

app.post('/create-post', function(request, response){
  var now = Date.now();
  var newpost = {
    timestamp: now,
    content: request.fields.blogpost
  }
  response.send(newPost);
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
