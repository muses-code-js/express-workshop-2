---
title: Troubleshooting
---


## Error: listen EADDRINUSE :::8080

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
Already have something running on that port.


## Error: Can't set headers after they are sent.

```
Error: Can't set headers after they are sent.
    at SendStream.headersAlreadySent (/home/dmison/NodeGirls/test/express-workshop-2/node_modules/send/index.js:390:13)
    at SendStream.send (/home/dmison/NodeGirls/test/express-workshop-2/node_modules/send/index.js:618:10)
    at onstat (/home/dmison/NodeGirls/test/express-workshop-2/node_modules/send/index.js:730:10)
    at FSReqWrap.oncomplete (fs.js:123:15)
```
You have express-formidable before express.static
