---
layout: step
number: 0
title: Setting up your Environment
permalink: step0/

keywords:
  - term: Fork
    define: A fork is a copy of a repository. Forking a repository allows you to freely experiment with changes without affecting the original project. Read more [here](https://help.github.com/articles/fork-a-repo/)

---

You have 2 options for setting up your environment. You can either go with setting up your environment locally, or
you can use [cloud9.io](https://c9.io). 

We encourage you to use [cloud9.io](https://c9.io) to complete this workshop as it comes with pre-configured workspaces
and allows you to start coding straight away. On the other hand, if you choose to work locally, you will need to configure 
a fully fledged environment on your own, starting with downloading Node. You will also need an editor if you work locally.
Please be aware of the fact that working locally might cause some issues in the case that there are any package dependency conflicts. 

Please choose your environment wisely and follow the instructions.

## Setting up your environment

* **For Local Environment** 

    Please download Node from the Node.js website [here](https://nodejs.org/en/). Make sure that you have an editor. 
    If you don't have one, we have a few suggestions for you; [Sublime](https://www.sublimetext.com/), [Atom](https://atom.io/), 
    [Brackets](http://brackets.io/). Choose whichever you prefer and follow the downloading steps. 

* **For Cloud9.io**

    :raising_hand: **If you don't have a cloud9.io account, please let any of the mentors know and we'll send you an 
    invitation to join our group space.**
    
    Start creating a new workspace. 
    
    Write your `Workspace Name`, `Description`, choose `Hosted workspace` as
    `Public`, skip the `Clone from Git or Mercurial URL` for now and choose `Node.js` as a template. Don't create
    the workspace yet, as we left the `Clone from Git or Mercurial URL` blank.
    
    Having an issue? Instructions for doing this can be found [here](https://docs.c9.io/v1.0/docs/create-a-workspace).

## Fork this repository
1. Go to the home page of [express-workshop-2](https://github.com/node-girls-australia/express-workshop-2) repository.
2. In the top-right corner of the page, click Fork. 
 
 That's it. Having an issue? Instructions for doing this can be found [here](https://help.github.com/articles/fork-a-repo/).
 
## Clone the repository in your environment
* **For Local Environment** 

    Clone your forked version of the repository to your desktop in the terminal. Instructions for doing 
    this can be found [here](https://help.github.com/articles/cloning-a-repository/), or run the command below.
    
    `$ git clone https://github.com/YOUR-USERNAME/express-workshop`
    
    This creates an express-workshop directory with the repository content inside. Change into the express-workshop directory, since that's where 
    we'll be working from now on.
    
    `$ cd express-workshop`
* **For Cloud9.io**

    Now paste the URL of your github forked repo `https://github.com/YOUR-USERNAME/express-workshop` in the
    `Clone from Git or Mercurial URL` field and hit the `Create workspace` button.
