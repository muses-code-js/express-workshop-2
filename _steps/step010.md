---
layout: step
number: 10
title: Saving New Posts (4/4)
permalink: step10/
keywords:
  - term: fs.writeFile()
    define: Asynchronously writes data to a file

---

You have come so far and we are finally ready for the last piece of the puzzle: saving your changes.  It has been a long and arduous road, but rest assured the end is in sight.

Thus far in our `/create-post` endpoint we have done the following:

1. Extracted our new post data and made a new object to hold it.
2. Read in the existing blogposts from disk, and updated that data.
3. Sent the new post object back as the reponse.

Now, between steps 2 and 3 we have to write it back to disk again.

## Writing to a file

To write to a file we use `fs.writeFile()`.  It's very similar to `fs.readFile()` except it writes to a file and it's parameters are a little different.

```javascript
fs.writeFile(path, data, callback)
```

The arguments to `writeFile()` are:

1. The **path** to the file to write to
2. The **data** you want to write to the file
3. A **callback** function to run after the write is complete.

The callback function for `writeFile` only takes one argument: an error object if the write failed or `null` if it was successful.

Here's where it can get confusing, because both `writeFile` and `readFile` are non-blocking.

This means that we have to call `writeFile` inside of the callback for `readFile` and send the response back in the callback function of `writeFile`.

Update the `readFile` callback of your `/create-post` endpoint like such:

```javascript
fs.readFile(__dirname+'/data/posts.json', function(error, data){
  if(error){
    console.log('Error reading posts.json: '+error);
    response.status(500);
    response.send(error);
  } else {
    var posts = JSON.parse(data);
    posts.blogposts.splice(-1, newPost);

    fs.writeFile(__dirname+'/data/posts.json', function(error){
      if(error){
        console.log('Error writing posts.json: '+error);
        response.status(500);
        response.send(error);        
      } else {
        response.send(newPost);              
      }
    });

  }
});
```

We also check the value of `error` in the `writeFile()` callback the same way we did for `readFile()`.  Just incase.

Once you have saved those changes, restart your server & try to make a new post.  It should appear in the page as expected, and if you refresh the page the posts should still be displayed.

Also you could open up the file `data/posts.json` in your editor and to see how it has changed.

If it isn't working for you, you can double-check that your code is right with the solution below.

Then head straight onto the next step.

```javascript
var express = require('express');
var formidable = require('express-formidable');
var fs = require('fs');

var app = express();

app.use(express.static('public'));
app.use(formidable());

app.post('/create-post', function(request, response){
  var now = Date.now();
  var newPost = {
    timestamp: now,
    content: request.fields.blogpost
  }

  fs.readFile(__dirname+'/data/posts.json', function(error, data){
    if(error){
      console.log('Error reading posts.json: '+error);
      response.status(500);
      response.send(error);
    } else {
      var posts = JSON.parse(data);
      posts.blogposts.splice(-1, newPost);
      console.log(posts.blogposts)

      response.send(newPost);
    }
  });
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
