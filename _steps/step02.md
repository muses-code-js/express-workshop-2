---
layout: step
number: 2
title: Installing Express
permalink: step2/

keywords:

  - term: npm install [package-name]
    define: The terminal command used to install a package from npm.

  - term: --save
    define: When added to the end of an `npm install` command, `--save` adds that npm package to the `package.json` file.

  - term: module
    define: A module is a bit of reusable code that can be imported into a Node.js project using the `require` function.

  - term: package
    define: One or more modules that is "packaged" and published to NPM.

---
In this workshop we are building a web server application. Node.js provides all the functionality to do this, but at a very low level.  You would need to make a lot of decisions about how to implement a server and then write that code and debug it.  It's a lot of work and it's also work that you have to do everytime you would write a web server application.  

Wouldn't it be great if someone had already done all that work?

Fortunately Node.js provides a way to publish code modules as `packages`.  People publish `packages` that solve particular common problems that they find themselves doing over and over.  So instead of you "re-inventing the wheel" everytime, you can use other people's packages and spend your time on what makes your application unique.  The packages that you install and use in your application are called its `dependencies`.

You can find published packages on the NPM website, <https://www.npmjs.com/>.  It currently has a little over half a million packages available.

`Express` is one such package that takes the drudge work out of building a web server application, and we are going to install and use it to build our application.  

## Installing Express

We use the tool `npm` to install dependencies.

Run the following command in your terminal:

```bash
npm install express --save
```

This command does the following steps:

1. Looks up the `express` package
2. Identifies all the dependencies of `express` and then all the dependencies of those dependencies and so on
4. Downloads *all* the packages identified in step 2 and puts them in a directory called `node_modules`
5. Updates `package.json` to include `express` and a version number in the `dependencies` section

If you look in `package.json` now you'll see a new section called `dependencies` with `express` listed in it:

```json
"dependencies": {
    "express": "^4.16.1"
  }
```

If you look in `node_modules` directory you will see a folder for each module.  You will see around 50 folders because in addition to `express` it also installed all of the modules used by `express` and all of the modules that they use, and all of the modules that those ones use and so on.  But it is smart enough to only download one copy of each.

So now we have `express` and all of it's dependencies installed, lets actually get on to writing some code.
