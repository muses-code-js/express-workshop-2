---
layout: page
title: Troubleshooting
permalink: troubleshooting/
---

Something not quite working right?

Here are some questions to that might help you.

 * Did you run the commands in the right directory?
 * Did you save your changes before starting the server?
 * Did you restart the server after saving your changes?
 * Do your brackets `[]`, parenthesis `()`, braces `{}`, quotes `''`, and double-quotes `""` all match up.  Generally they are always in pairs.
 * Have you tried adding some `console.log()` statements to the code in question to check that variables have the values you expect?
 
## Error Messages

Here are some error messages you might encounter with this and a possible solution.

#### Error: listen EADDRINUSE :::8080

```
events.js:160
      throw er; // Unhandled 'error' event
      ^

Error: listen EADDRINUSE :::8080
    at Object.exports._errnoException (util.js:1020:11)
    at exports._exceptionWithHostPort (util.js:1043:20)
    at Server._listen2 (net.js:1258:14)
    at listen (net.js:1294:10)
    at Server.listen (net.js:1390:5)
    at EventEmitter.listen (/home/ubuntu/workspace/node_modules/express/lib/application.js:618:24)
    at Object.<anonymous> (/home/ubuntu/workspace/server.js:8:5)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
    at Module.load (module.js:487:32)
```
Already have something running using that port.  Do you have another terminal open with your app already running?  Make sure you stop that one first.


#### Error: Can't set headers after they are sent.

```
Error: Can't set headers after they are sent.
    at SendStream.headersAlreadySent (/home/dmison/NodeGirls/test/express-workshop-2/node_modules/send/index.js:390:13)
    at SendStream.send (/home/dmison/NodeGirls/test/express-workshop-2/node_modules/send/index.js:618:10)
    at onstat (/home/dmison/NodeGirls/test/express-workshop-2/node_modules/send/index.js:730:10)
    at FSReqWrap.oncomplete (fs.js:123:15)
```
You are probably trying to use `express-formidable` before `express.static` in step7.  Make sure you have them in the correct order. 
