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

** III ** SSH key.

We all know the usual to connect to the server will need a username and password. With git, to connect to its server authentication server machine using ssh key with you.

ssh key will have 2 key, a private key and a public key. You will create the 2 key in your computer and put the server containing the public key repo that you want to connect to. So your computer has been authenticated. After this each time you take the code from the server, or put code on the server will not need to enter username and password again.

Unfortunately your computer contains important repo and if you miss someone steals your computer. You do not want people to intervene and your repo, only the repo on the server and delete public key is finished. We can generate SSH key as follows:

{% highlight Bash shell scripts linenos%}
- Launch Gitbash
- cd ~ / .ssh
- ssh-keygen -t rsa -C "youraddress@email.com" (Skip name)
- Open the file "id_rsa.pub" in the directory "C: \ Users \ <name> \. Ssh", copy the contents into your Github account on the server: https://github.com/settings/ssh (Login Add SSH key)
- Test check: ssh -t git@github.com (If you receive the message "Hi username! You've successfully authenticated, but does not cung shell access Github." Means that the installation was successful.
{% endhighlight %}

Nếu không muốn tạo SSH key ta có thể tạo 1 file tự nhập pass word mỗi lần commit( Tôi đang dùng cách này) . Ta tạo file .netrc với nội dung:
{% highlight Bash shell scripts linenos%}
- machine github.com
  login <account github>
  password <password>
{% endhighlight %}
** IV ** The command or use the git.
After Git client is installed and configured correctly, the next step is to initialize Git on your personal computer and create truly interactive to Github.
 **First part** Initialize the repo directory on the client machine (computer programmer)
{% highlight Bash shell scripts linenos%}
mkdir C:\<Name repo>
cd <Name repo>
git init
{% endhighlight %}
**First 2** Connect to Github repo
{% highlight Bash shell scripts linenos%}
git remote add remote_name git@github.com: (Name repo)
{% endhighlight %}

**First 3** Keep the content from the server before downloading new content from the client to
{% highlight Bash shell scripts linenos%}
git pull git@github.com: (Name repo) master
{% endhighlight %}

**First 4** Check the status change
{% highlight Bash shell scripts linenos%}
git status
{% endhighlight %}

**First 5** Put the file in the list before commit (skip if no new file is created)
{% highlight Bash shell scripts linenos%}
git add. (Add all the files that have changed)
git add <file path> (Add 1 file)
{% endhighlight %}

**First 6** Commit the changes before pushing up server
{% highlight Bash shell scripts linenos%}
git commit -a -m "brief info about this change" (-a All change)
{% endhighlight %}

**First 7** Upload accelerating the development server
{% highlight Bash shell scripts linenos%}
git push <remote-name> <branch-name>
eg: git push abc work
{% endhighlight %}

**First 8** Upload server master branch
{% highlight Bash shell scripts linenos%}
-u git push origin master
{% endhighlight %}

**First 9** See all branches are
{% highlight Bash shell scripts linenos%}
git branch -a
{% endhighlight %}

**First 10** Create a new branch
{% highlight Bash shell scripts linenos%}
git branch <new name>
{% endhighlight %}

**First 11** Transfer Branch
{% highlight Bash shell scripts linenos%}
git checkout <branch name>
{% endhighlight %}

**First 12** Remove branches
{% highlight Bash shell scripts linenos%}
git branch -d <branch name>
