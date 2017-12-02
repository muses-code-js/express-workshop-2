---
layout: challenge
cnumber: 1
title: Mood Indicator
permalink: challenges/1/
difficulty: 1
---

This challenge adds a menu to to pick a "mood" (happy,sad, angry etc) from a list when making a post.  That mood is then displayed on that post.

<!--BREAK-->

## 1. Enabling the UI

First up we have some changes to the UI.

To add these changes do the following steps:

1. Open up `public/main.css`

    Find the line `/* 1. mood indicator */`.

    Insert the following code after that line:

    ```css
    @font-face {
      font-family: "NotoColorEmoji";
      src: url("NotoColorEmoji.ttf");
      text-decoration: none;
      font-style: normal;
    }

    div.mood {
     margin: 5px;
     font-size: 18px;
    }

    div.mood .emoji {
     font-family: "NotoColorEmoji";
     font-size: 30px;
    }

    div.mood-select {
     margin: 25px 15px;
     font-size: 20px;
     display: inline-block;
    }

    @media screen and (max-width: 600px) {
      div.mood-select {
        margin: 15px 20px 0px 20px;
      }
    }
    ```

2. Open up `public/script.js`

    Find the line `// 2. insert mood display here`.

    Insert the following code after that line:

    ```javascript
    var moodNames = [
      "",
      "<span class='emoji'>😃</span> Happy",
      "<span class='emoji'>😛</span> Joking",
      "<span class='emoji'>😢</span> Sad",
      "<span class='emoji'>😔</span> Regretful",
      "<span class='emoji'>😡</span> Angry",
      "<span class='emoji'>😲</span> Suprised",
      "<span class='emoji'>😎</span> Smug",
      "<span class='emoji'>👑</span> Triumphant",
      "<span class='emoji'>😍</span> In love"
    ];
    var moodDiv = document.createElement("div");
    moodDiv.className = "mood";
    moodDiv.innerHTML = moodNames[post.mood];
    postText.append(moodDiv);
    ```


3. Open up `public/index.html`

    Find the line `<!-- 3. mood selector -->`.

    Insert the following code after that line:

    ```html
    <div class='mood-select'>I'm feeling:
      <select name='mood'>
        <option value='0'>None</option>
        <option value='1'>😃 Happy</option>
        <option value='2'>😛 Joking</option>
        <option value='3'>😢 Sad</option>
        <option value='4'>😔 Regretful</option>
        <option value='5'>😡 Angry</option>
        <option value='6'>😲 Suprised</option>
        <option value='7'>😎 Smug</option>
        <option value='8'>👑 Triumphant</option>
        <option value='9'>😍 In love</option>
      </select>
    </div>
    ```

Make sure you save those changes & refresh the web page.  You should see the "Mood" menu near the `POST` button.

It will look like this:

![Mood feature enabled]({{'/assets/challenge-2a.png' | relative_url }}){:title="Mood feature enabled" class="img-responsive imgbox"}

With the above changes, the webpage now does the following:

1. When creating a new post, it sends a value of 0 to 9 as the field `mood` as part of the form data.
2. Expects the blogpost objects retrieved from `/get-posts` to each have a mood property, with a value of 0 to 9, for which it displays the corresponding mood emoji and description.

Once properly implemented posts with a mood set will look like this:

![Post with Mood set]({{'/assets/challenge-2b.png' | relative_url }}){:title="Post with Mood set" class="img-responsive imgbox"}


## Backend Specification

The following changes are required:

1. `/create-post` receives an additional form data field, `mood` which must be saved as part of the post object.
2. The post objects returned by `/get-posts` should include a mood property. Example:

    ```json
    {
      "timestamp": "2342423432233",
      "content": "This is a new post",
      "mood": "3"
    }
    ```

## Hints

1. Remember you can use `console.log()` to check how the contents of variables or parameters change.
2. You will only need to change the `/create-post` endpoint to ensure that the mood data is saved.  
3. `/get-posts` returns all the information regardless so no changes are required there.

## Solution

If you get stuck or just want to compare with your answer click below to see our solution.

Note that this solution only shows the endpoint in question, not all of `server.js`.

```javascript
app.post("/create-post", function(request, response){
  var now = Date.now();
  var newPost = {
    timestamp: now,
    content: request.fields.blogpost,
    mood: request.fields.mood
  }

  fs.readFile(__dirname+"/data/posts.json", function(error, data){
    if(error){
      console.log("Error reading posts.json: "+error);
      response.status(500);
      response.send(error);
    } else {
      var posts = JSON.parse(data);
      posts.blogposts.push(newPost);

      var updatedData = JSON.stringify(posts);

      console.log(posts);
      console.log(updatedData);

      fs.writeFile(__dirname+"/data/posts.json", updatedData, function(error){
        if(error){
          console.log("Error writing posts.json: "+error);
          response.status(500);
          response.send(error);
        } else {
          response.send(newPost);
        }
      });
    }
  });
});
```
{: .solution }

Remember just because your solution doesn't look exactly like this one doesn't mean that it is wrong.  The important question is whether it works or not.  If your answer is very different you might want to ask a mentor in case you are doing something that looks like it works but will create problems for you later.
