---
layout: post
title:  "Welcome to my new technical blog!"
date:   2019-05-16 10:58:08 +0100
categories: frontend
permalink: /:categories/welcome
---
This post is to start the new version of my blog. To do this, I move on from wordpress to git pages. So, my technical posts are going to be here. The other posts are going to continue on wordpress.

Then, to start this, I wached the overview in a Udemy [here](https://www.udemy.com/github-pages/learn/v4/overview). It's so simple but is great to have an ideia about [GitHub Page](https://pages.github.com/).

<h3>Steps</h3>

The first step is to create an account on github, of course. After that, you have to create a repository with your username followed by 'github.io'. The next step you need to have some tool to manage the repository. I downloaded the [GitHub Desktop](https://desktop.github.com/). To edit the files I am using the [Atom](https://atom.io/).

To help you with your pages you can use [Jekyll](https://jekyllrb.com/) that is integrated with GitHub Pages. There is great [tutorial](https://jekyllrb.com/tutorials/video-walkthroughs/) that will help you to get an overview of the Jekyll. If you use MacOS, like me, you need be sure about the version of ruby. Jekyll need the version 2.4 installed. For more detail you can read that [here](https://jekyllrb.com/docs/installation/macos/).

<h3>Facilities</h3>

Using the jekylls you can do everything you can do using other tools. You  can find themes and edit them. Maybe you can have a more work to do and to learn, but It makes you have more control of your pages using a free account and tools.

 <h3>Main commands</h3>

The Jekyll has some basic commands to help you to manipulate your project. After you create your project it will be create a structure of the page and some configuration files where you will update themes, title, content, etc. The available themes to github you can find [here](https://pages.github.com/themes/).

{% highlight ruby %}
#create new project. Can be the same that you cloned from git
gem new username.github.io

# To execute
bundle exec jekyll serve

{% endhighlight %}

<h3>Other commands</h3>

If your variables environment is not configured, maybe you need other commands to start your application;

{% highlight ruby %}
export PATH=/usr/local/opt/ruby/bin:$PATH
export PATH=$HOME/.gem/ruby/2.6.0/bin:$PATH
bundle exec jekyll serve
{% endhighlight %}

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
