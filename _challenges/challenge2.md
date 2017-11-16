---
layout: challenge
cnumber: 2
title: Deleting Posts
permalink: challenges/2/
difficulty: 4
keywords:
  - term: Route parameters
    define: |
      Route parameters are a way to create routes where specified parts of the URL can have any value, and you can access those values in the route's handler function.  [Express Routing Guide](https://expressjs.com/en/guide/routing.html)
  - term: DELETE request method
    define: |
      The DELETE request method indicates that a request is intended to result in data being deleted by the server.
       [MDN HTTP docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
  - term: Array.filter()
    define: A function on array objects that lets you create another array that contains subset of the current one. [MDN Array.filter() docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
---

This challenge adds the ability to delete posts to your app.

<!--BREAK-->

## 1. Enabling the UI

First up we have some changes to the UI to add a delete button to each post.

To add these changes do the following steps:

1. Open up `public/main.css`

    Find the line `/* 1. delete button styles */`.

    Insert the following code after that line:

    ```css
    .delButton {
    	display: inline;
    	float: right;
    	color: rgba(200,0,0,0.5);
    }

    .delButton:hover {
    	color: rgba(200,0,0,1);
    	cursor: pointer;
    }
    ```

2. Open up `public/script.js`

    Find the line `// 2. delete post function`.

    Insert the following code after that line:

    ```javascript
    function deletePost (timestamp) {
      fetch('/delete-post/'+timestamp, {
          method: 'DELETE'
      })
      .then(function (res) {
          res.json()
          .then(function (json) {
            if(json.success){
              var element = document.getElementById(timestamp);
              element.outerHTML = "";
              delete element;
            } else {
              alert('Delete failed!');
            }
          });
      })
      .catch(function (err) {
        alert('Delete failed!\n\n'+err);
      });
    }
    ```

2. Open up `public/script.js`

    Find the line `// 3. insert delete button here`.

    Insert the following code after that line:

    ```javascript
    var delButton = document.createElement('div');
    delButton.onclick = function(){
      if (confirm('Are you sure you want to delete this post?  You can\'t undo this.')){
        deletePost(post.timestamp);
      }
    }
    delButton.className = 'delButton'
    delButton.innerHTML = '<i class="fa fa-trash-o" aria-hidden="true"></i> Delete';
    postDetail.appendChild(delButton);
    ```

Make sure you save those changes & refresh the web page.  You should see the delete link at the bottom of each post.

It will look like this:

![Delete feature enabled]({{'/assets/challenge-1a.png' | relative_url }}){:title="Delete feature enabled" class="img-responsive imgbox"}

## Backend Specification

To implement the delete feature in the backend, you need to create an endpoint for deleting a post.  This endpoint has the following requirements:

 * Endpoint URL: `/delete-post/:timestamp`
 * Request Method: DELETE
 * It needs to delete the post from `posts.json` with the matching timestamp and make sure the file is saved.
 * If no error occurs, the expected response is `{ "success": true }`
 * If an error occurs, the expected response is `{ "success": false }`

**Hint:** This endpoint will be very similar to `/create-post` as you will need to read `posts.json` in, do some updates, and then save that file again.

## Route Parameters

Route parameters are a way to create routes where specified parts of the URL can have any value, and you can access those values in the route's handler function.  

You can do this by prefixing a URL segment (bit between each pair of `/`) with a colon `:`.

Each of those route parameters will be available as a property of `request.params` with the corresponding name.

As an example:

```javascript
app.get('/say/:name/:phrase', function(request, response){
  response.send(request.params.name + ' says "'+request.params.phrase+'"' );
});
```

`/say/sarah/giraffe` will respond with `sarah says "giraffe"``

`/say/sarah` will not match this route.

Route parameters are a great way to both use the URL to pass information in the request, and to make your apps URL's more meaningful.

## The DELETE request method

The DELETE request method indicates that this request expects to result in data being deleted.

Just like GET and POST there is a corresponding Express function for creating DELETE routes.

## Array Filtering

There are several different techniques you can use to remove items from an array.  `Array.filter()` is probably the most powerful, but it might seem strange at first.

`Array.filter()` lets you makes a new array by taking an existing one and choosing elements from it to include in the new one.  You can then use that array in place of the old one.  

Lets demonstrate it with an array of names.  We want to remove the names from the array that have 5 or less letters.  

```javascript
// original array
var names = [ 'Michael', 'Susan', 'Angelica', 'David', 'Joe'];

// making a new array using filter
var filteredNames = names.filter( function(name){
  return name.length > 5;   //only include those longer than 5 letters
} );

// assign filteredNames as the new value of names
names = filteredNames;

console.log(names);
```

If you run this code you will see the output of:

```
[ 'Michael', 'Angelica']
```

`Array.filter()` chooses the elements to include using a "rule" that you give it.  This rule is the function that you pass to `filter()`.  

`Array.filter()` runs that function once for each element of the array, passing the array element as a parameter.  Within that function you can do whatever you want to determine if you want to keep that element or not.  If the function returns `true` then that means the element should be kept.  `false` means don't keep the element.  

You could also do the assignment and filter in one step like this:

```javascript
var names = [ 'Michael', 'Susan', 'Angelica', 'David', 'Joe'];

names = names.filter( function(name){
  return name.length > 5;
} );

console.log(names);
```

It is important to note that although `Array.filter()` runs this "rule" function for every element in the array it does them all at the same time.  This makes it fast even for very large arrays. 

Remember `filter()` doesn't change the original array, it creates a new one with only the items to keep from the first.  So you will have to remember to explictily do something with your new array.


## Hints

1. You'll be creating a new endpoint, that will probably be very similar to `/create-post`
2. It will be a DELETE request
3. You'll need to use route parameters to indicate which post is to be deleted
4. `Array.filter()` is an easy way to remove items from an array
5. Don't forget you can use `console.log()` to check the values of variables.

## Solution

If you get stuck or just want to compare with your answer click below to see our solution.

Note that this solution only shows the endpoint in question, not all of `server.js`.

```javascript
app.delete('/delete-post/:timestamp', function(request, response){

  // read our file in
  fs.readFile(__dirname+'/data/posts.json', function(error, data){
    if(error){
      console.log('Error reading posts.json: '+error);
      response.status(500);
      response.send(error);
    } else {
      var posts = JSON.parse(data);

      // filter out post with same timestamp value as request.params.timestamp
      posts.blogposts = posts.blogposts.filter(function(post){
        return post.timestamp != request.params.timestamp;
      });

      // stringify and write to disk
      updatedData = JSON.stringify(posts);
      fs.writeFile(__dirname+'/data/posts.json', updatedData, function(error){
        if(error){
          console.log('Error writing posts.json: '+error);
          response.status(500);
          response.send(error);
        } else {
          response.send({success: true});
        }
      });
    }
  });

});
```
{: .solution }

Remember just because your solution doesn't look exactly like this one doesn't mean that it is wrong.  The important question is whether it works or not.  If your answer is very different you might want to ask a mentor incase you might be doing something that looks like it works but will create problems for you later.
