---
layout: post
title: "Blog=Github+Octopress"
date: 2014-04-24 22:44:20 +0800
comments: true
categories: 
---
Why I write blogs
------------------
Actually, I am not a blog heavy writer. I use blog most as a tool to write down my thoughts, my experience and my notes.

Why I choose Github and Octopress
----------------------------------
A blog should provides following functions as I see:

1. Full freedom to control content of all blog post, ease to access and migrate the content. [Github][gh] is an ideal place to host a blog for it provides free disk space and free version control service, and most of all it is becoming the facebook for hackers.
[gh]:github.com

2. Ability to embed code snippets. [Jekyll][jk] and [Octopress][oc] both suit.
[jk]:jekyllrb.com 
[oc]:octopress.org

3. Ability to support latex. This is what I really like. 

How I built up this blog
------------------------
There are many blog posts that guides how to build up a blog with Github and Octopress, links below are where I have got tips from:

1. [ChuChao333][]
2. [dblock][]
3. [gerardcondon][]
4. [octopress][]

[ChuChao333]:http://chuchao333.github.io/blog/2012/07/25/octopress-and-github/
[dblock]:http://code.dblock.org/octopress-setting-up-a-blog-and-contributing-to-an-existing-one
[gerardcondon]:http://www.gerardcondon.com/blog/2012/03/04/setting-up-octopress-and-github/
[octopress]:octopress.org


Below are my steps:

Install Ruby
------------
Octopress is a blogging framework based on Jekyll and which is written in Ruby. I am very new to Ruby, so I just followed other's introduction to install Ruby by [RVM][].

RVM(Ruby Version Manager), as its name says, is a software platform designed to manage multiple installations of Rury on the same device. Before installing RVM, we need to check whether following softwares are already installed.
{% highlight shell %}
bash, awk, sed, grep, ls, cp, tar, curl, gunzip, bunzip2, git, svn
{% endhighlight %}

After requirements were meet, use following command to install RVM:
{% highlight shell %}
caojinghua@debian:~$ \curl -sSL https://get.rvm.io | bash -s stable --ruby
{% endhighlight %}
Above is the Single-User installation, which means the rvm is installed in the current user's home directory, that is '~/.rvm'. After this, we should use following command to load RVM:
{% highlight shell %}
caojinghua@debian:~$ source ~/.rvm/scripts/rvm
{% endhighlight %}
Use following command to test whether RVM is installed successfully:
{% highlight shell %}
caojinghua@debian:~$ type rvm | head -n 1
{% endhighlight %}

After RVM was installed, we install Ruby 1.9.3 as follows:
{% highlight shell %}
caojinghua@debian:~$ rvm install 1.9.3
{% endhighlight %}

We set this version of Ruby to use as the default for new shells:
{% highlight shell %}
caojinghua@debian:~$ rvm use 1.9.3 --default
{% endhighlight %}

To test whether Ruby was installed successfully:
{% highlight shell %}
caojinghua@debian:~$ ruby -v
{% endhighlight %}

[RVM]:rvm.io

Install Octopress
-----------------
Clone the git repository of Octopress:
{% highlight shell %}
caojinghua@debian:~/myworkstation$ git clone git://github.com/imathis/octopress.git octopress
caojinghua@debian:~/myworkstation$ cd octopress/
{% endhighlight %}

Next, install Octopress's dependencies:
{% highlight shell %}
caojinghua@debian:~/myworkstation/octopress$ gem install bundler
caojinghua@debian:~/myworkstation/octopress$ bundle install
{% endhighlight %}
It was the last command that I have wait a long time for, due to my unstable network speed.

Next, install Octopress's default theme: 
{% highlight shell %}
caojinghua@debian:~/myworkstation/octopress$ rake install
{% endhighlight %}

By now we have installed Octopress successfully.

Create a new repository in GitHub for the blog
----------------------------------------------
We need a repository in GitHub that stores all static web pages and source files of the blog, and Github would show these pages in such an URL: *uername*.github.io, where *username* is the name of your Github account, and the repository's name should follow this format: *username*.github.io.

Configure Octopress to the Github repository
--------------------------------------------
The octopress repository we installed previouly contains several tasks to generate our blog. Use following task to generate a blog:
{% highlight shell %}
caojinghua@debian:~/myworkstation/octopress$ rake setup_github_pages
{% endhighlight %}
Several things were done in this command:

1. Since the remote origin points to "git://github.com/imathis/octopress.git", it set up a new remote reference name "octopress" that points to "git://github.com/imathis/octopress.git".
2. Change the remote origin points to "git@github.com:*username*/*username*.github.io.git", so as to attach to the github repository while doing "git pull or git push" commands.
3. Rename octopress repository's master branch to "source". So while doing "git push origin source", all updated objects in the local source branch would be pushed into the remote github repository(*username*.github.io)'s source branch. And we have successfully make the local octopress source branch mapping to the remote *username*.github.io repository's source branch. Each time we have update in this source branch, we should push it to the corresponding remote branch.
4. Create a directory "_deploy" within the octopress directory, and git clone the *username*.github.io repository's master branch into this "_deploy" directory. "_deploy" directory contains all files generated by octopress and that are ready to show as web pages. Each time we have updated blog post, we should regenerate files, and git push "_deploy" directory's files to remote *username*.github.io 's master branch, that's where Github grap web pages from to show our blog.

Generate post and deploy
------------------------
Now, all is ready. We use following task to generate a new post:
{% highlight shell %}
caojinghua@debian:~/myworkstation/octopress$ rake new_post["*title*"]
{% endhighlight %}

Use following task to regenerate all files:
{% highlight shell %}
caojinghua@debian:~/myworkstation/octopress$ rake generate
{% endhighlight %}
This task would scan files within "source" directory, and output all generated files in "public" directory. After that, we should git push updated contents to remote *username*.github.io 's source branch by:
{% highlight shell %}
caojinghua@debian:~/myworkstation/octopress$ git add .
caojinghua@debian:~/myworkstation/octopress$ git commit -m "blog post update"
caojinghua@debian:~/myworkstation/octopress$ git push origin source
{% endhighlight %}

Next, we can deploy our blog by:
{% highlight shell %}
caojinghua@debian:~/myworkstation/octopress$ rake deploy
{% endhighlight %}
This task would commit all updated content in "_deploy" directory, and git push it to the remote *username*.github.io 's master branch.

Summary
-------
I think several ponts are important during this building process:

1. Master git, at least understand the essence of git.
2. Try to use ssh to connect to github repository.
3. Patience is needed.
 
