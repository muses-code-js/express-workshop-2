---
layout: step
number: 0
title: Setting up your Environment
permalink: step0/

keywords:
  - term: Fork
    define: A fork is a copy of a repository. Forking a repository allows you to freely experiment with changes without affecting the original project. Read more [here](https://help.github.com/articles/fork-a-repo/)
  - term: Cloud9
    define: Web-based development environment. See <https://c9.io>
  - term: Terminal
    define: shell to run commands
  - term: Editor
    define: program to edit text files
  - term: Integrated Development Environment (IDE)
    define: software suite containing editor, terminal, and other tools

---
Ok before you get started coding you need to setup all the things that you are going to need.

We need:

 - Node.js dev Environment
    - The Node.js **runtime**
    - An appropriate editor
    - A terminal (to run commands)

- Also we will setup a Github account.  
  
## GitHub

[GitHub.com](https://github.com) is a web site that makes it really easy for multiple people to share and work on the same projects together using a program called **Git**.  Git provides you with a way of tracking all the changes that you make to your project.

Git is a pretty big topic that we aren't going to explain too much here. We are just going to use it to make a couple of things a bit easier to setup.  

So don't worry too much about understanding all the git stuff right now.  That said however, git is *very* popular and widely used both in companies and open-source projects,  so we highly recommend that you spend some time learning about it after the workshop.

We are going to create a GitHub account & "fork" the `express-workshop-2` repository.  This means you will get a copy of all the workshop files in your GitHub account.  Repostory is just another name for a set of files and folders being managed by Git.

### Create a GitHub Account

1. Go to [GitHub.com](https://github.com) and follow the prompts to create an account there

### Fork the Repository

1. Go to <https://github.com/node-girls-australia/express-workshop-2>
2. Click the `Fork` button on the top right.

This will take a moment, and then you will be redirected to your new copy of the repository.

Don't worry too much if you didn't understand what happened there.  The key thing is that you now have a copy of the workshop files in GitHub.

## Development Environment

To create software using Node.js you need three things:

1. The Node.js **runtime**
2. An editor
3. A command-line terminal (to run commands in)

You *can* download and setup these things on your own computer but it can be tricky and time consuming even if you have experience doing this kind of thing.  It depends a lot of your computer and what Operating System and other software you already have installed.  

To save time, we recommend using [Cloud9](https://c9.io), an online service that provides all of those things preconfigured as a web application.


### Cloud9

Cloud9 is a web site that provides an online development for several languages including Node.js.  You can access it using just a web browser which makes it really easy to get started. 

#### Create a Cloud9 account

1. Ask a mentor to send you an invite to the Node Girls Cloud9 team.  This only takes a few minutes.
2. When you receive the invitation email, click on the link and follow the promps to setup an account.

#### Connect Cloud9 to GitHub
Once you are logged into your Cloud9 account, you can connect it to your GitHub account so you can use Cloud9 to access your copy of the workshop.

1. Click repositories.  
2. Click Connect on GitHub item, and follow the prompts to authenticate Github.

Now the Repositories page should should a list of your GitHub repositories including your `express-workshop-2` repository.

#### Creating a Cloud9 Workspace

Workspaces are how Cloud9 organises projects.  Think of each workspace as the UI for interacting with your project, editing the files and running commands etc.

We will create a new workspace which will let you work on the files from your `express-workshop-2` git repository.

1. Go to your Repositories page in cloud9 and find the entry for `express-workshop-2`
2. Click on the Clone to edit button
3. On the `Create a new workspace` page:
    * Enter a name for the workspace
    * Select the Node.js template
    * Click Create Workspace  

Cloud9 sets up the workspace and opens it for you with the "Welcome Page" open.

![Fresh new Cloud9 workspace]({{ '/assets/step0-a.png' | relative_url }}){:title="Fresh new Cloud9 workspace" class="img-responsive imgbox"}

The three main areas you need to know about are: 

1. The **workspace file view** on the left where you can see all the files in your project.  Double-clicking on a file will open it in the editor view.
2. The **editor view** takes up the main space in the middle.  It is where you edit your source code.  Each file opens in a new tab here.
3. The **terminal tab** at the bottom.  This is the command line space where you will run various commands during the workshop such as installing packages and running your code.

You can rearrange this space as you see fit, and also add and remove items from it.  If you need to get back to the original layout, you can do this by going to the main menu and selecting `Window -> Presets -> Full IDE`.  

### Local Machine

If you want to take the leap of setting things up on your own computer, you will need to do the following:

1. Install Node.js
2. Install an Editor
3. Install Git (Optional)
4. Download the workshop files

#### Install Node.js

You can download the Node.js installer from <https://nodejs.org/en/download/>  

Download it, run it and follow the prompts.

There are installers for Windows, macOS & Linux.  Linux users should check if their distro includes a Node.js package for easy installation.

The most recent version of Node.js at time of writing is 8.  However any release of 6 or greater should work fine.

Once Node.js is installed, open a terminal and enter the command `node --version` to verify that it is installed correctly.

![Confirming Node.js install on Windows]({{ '/assets/step0-b.png' | relative_url }}){:title="Confirming Node.js install on Windows" class="img-responsive imgbox"}


#### Install an Editor

#### Install Git (Optional)

#### Download the workshop files 


