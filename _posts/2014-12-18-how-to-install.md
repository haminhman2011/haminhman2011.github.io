---
layout: post
title: Github overview
categories: articles
tags: [sample-post]
comments: true
description: Github overview
---

![Elaphurus davidianus](http://labs.septeni-technology.jp/wp-content/uploads/2013/08/github-bi-hack.jpg "Père David's deer")

** I ** What is Github?

Github http://github.com, also known as social network for developers put into operation in February 2008, is a service management system using distributed GIT help users to store source code for the project project. Features of GIT has all the features of a source control like SVN and more.

Github is written in Ruby on Rails. GitHub offers both commercial and free accounts for open source projects. According to a survey of the use Git in 2009, is currently Github Git hosting server source code most popular now (Also, Gitorious http://gitorious.org Git server as well as activities like Github attention to).

439,000 developers to create more than 1 million 350 thousand repositories is an impressive figure, along with a large number of customers github as Twitter, Facebook, Yahoo ... shows the popularity of Github, community programming and computer world how responsible it.

** II ** The way to work with GitHub.
Working with GitHub GIT system in particular or in general there are two local workflow workflow and workflow server.

You can make things change in a local source code, after the change is complete, but you will commit changes to the server and the server version is the complete version a certain feature or bug fix is complete, test finished or at least that version to run. Do not commit unfinished code, not through the test server to the repository will affect other members, otherwise you can do it in a local repository (You can also create a branch in the code server to commit in progress or unfinished features as worked with SVN, it will occupy space on the server as well as take your time to interact with the server connection, so why not commit it to the local repository, right, just fast operation did not take the server space.)

Open wide: from the github repository can be in the form of creating builds for production Git site (this is a repository on the server) by push changes (over thoroughly test) to it.
When interacting with the repository server (update or change) GitHub code requires certification "Who Are You" by comparing SSH key in your local server and SSH key corresponding to the account you signed up with GitHub before.

 **First part** Working with local repository at: 2 command is used git add and git commit
 - git add: add file has changed on stage
 - git commit: commit files to add to the stage in a local repository
Also you see some other command
**First 2** Working with server repository at github:
Once in the local code, the last time a stable and complete (through testing), we will decide to update it to the repository server with:
-push: push changes from repository to repository server local
-fetch: updated changes from repository to repository local server
-pull / rebase: copy the source code from the server to your local workspace (the equivalent of SVN checkout)

