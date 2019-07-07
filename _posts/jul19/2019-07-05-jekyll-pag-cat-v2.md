---
layout: post
title:  "Jekyll - Pagination and Category - V2"
date:   2019-07-05
categories: jekyll
permalink: /:categories/jekyll-pag-cat-v2
---

This post will show you how I improve my first version of my blog. I am using Jekyll with GitHub and my first version uses the minima theme in a simple way. The second version I added pagination and category.

<center>
  <img src="/img/jekyll/version1.png" width="556" height="400">
</center>

<br/>

<h3>What is Jekyll</h3>

> Jekyll is a simple, extendable, static site generator.

The Jekyll was created with [Ruby][ruby-ref], then, to use that you'll need to have the Ruby in your machine. The first step you can see [here][QuickStart-ref]. The menu on the right side there is two important links ([Ruby101][ruby101-ref] and [Installation][installation-ref]) that will help you on your configuration.  You don't need to be an expert in ruby because the site will give you enough information.

After that, you will find many [resources][resources-ref] such as plugins and editors That you can to add to make easier your work. The editor that I am using is the [markdown][markdown-ref] because I am using the atom to work on my blog.

<h3>Main Concepts</h3>

**Liquid** is the first concept. It is a templating language that you permit you to manipulate object, tags and filters on the pages.

**Front matter** is such a config header of your page. You have to have this to indicate the title, category, date, any variable that you need.

Also you can have **layout**, **include** tag, **data files** (CSV, JSON, etc), **assets** (CSS, images, js), **blogging** (list of posts) and **Collections**.

The posts have to be inside of the \_post folder, each post must have **front matter** and the names' post must have a filename with the publish date, a title, and an extension. It's a great practice is to use categories to organize the posts.

The detail about these components you will find on [Step by Step][step-by-step-ref].

Another important concept is the [directory structure][structure-ref] with folder and pages organization. The reserved folder will start with '\_'. When you use a theme and want to customize this you need to follow the same structure.

Moreover, exist [variables][varible-ref] that are very helpful to manipulate the data from your blog. The scope can be global, site or page.

And the last but not least, if you want to use a theme, Jekyll has many options, but to use in GitHub there are just a few numbers of [theme possible][theme-ref].

The theme that I'm using in my blog until the moment of this blog is [minima][minima-ref].

<h3>Pagination</h3>

In some moments you will feel the necessity to [paginate][pagination-ref] your blog. In my case, I am using a plugin to Jekyll, the [jekyll-paginate-v2][pagination-plugin-ref] plugin.  

The first step to use the plugin is to install it by command line and then to add the reference in the Gemfile.

{% highlight ruby %}
# command line
$gem install jekyll-paginate-v2
# Gemfile
gem "jekyll-paginate-v2"
{% endhighlight %}

Now, to use the pagination, I follow theese [examples][pagination-examples-ref]. I configurated the [\_config file][config-file-ref]. My [config file][my-config-ref] is like below.

{% highlight ruby %}
# \_config.yml

plugins:
  - jekyll-feed
  - jekyll-paginate-v2

pagination:
  enabled: true
  per_page: 5
  permalink: '/page/:num/'
  title: ':title - page :num'
  limit: 0
  sort_field: 'date'
  sort_reverse: true
  trail:
    before: 2
    after: 2
{% endhighlight %}

Now, the site is prepared to use the pagination. I created a separate file inside the **\_includes** folder. The file is [postsByCategory.html][postsCat-ref]. It will list all my posts on the page. The specific code to paginate in the second version of my blog, based on the examples, is:

{% highlight ruby %}
{ % if paginator.total_pages > 1 % }
  <ul class="pager">
      { % if paginator.first_page % }
          <a href="{ { paginator.first_page_path | prepend: site.baseurl | replace: '//', '/' } }">First</a>
      { % endif %}

      { % if paginator.previous_page % }
          <a href="{ { paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' } }">&larr; Newer</a>
      { % endif %}

      { % if paginator.page_trail % }
        { % for trail in paginator.page_trail %}
          | <a href="{ { trail.path | prepend: site.baseurl | replace: '//', '/' } }" title="{ {trail.title} }">{ { trail.num } }</a>
        { % endfor %}
      { % endif %}

      { % if paginator.next_page % }
      |  <a href="{ { paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' } }">Older &rarr;</a>
      { % endif %}

       { % if paginator.last_page % }
      |   <a href="{ { paginator.last_page_path | prepend: site.baseurl | replace: '//', '/' } }">Last</a>
      { % endif % }
      |
  </ul>
  { % endif %}
{% endhighlight %}

I included this page inside of my [index page][index-ref] that doesn't have any category declared, but has the pagination tag explicitly enabling the page to the pagination.

{% highlight ruby %}
---
layout: home
pagination:
  enabled: true
---
{ % include postsByCategory.html % }
{% endhighlight %}


<h3>Category Menu</h3>

Another important point is the category. Show posts by category. To do this, I got examples from [navigation doc][nav-ref] and [webjeda][webjeda-ref].

In the same [postsByCategory.html][postsCat-ref] file there is a complementary code to filter by category. Also, the posts have to have a category declared. For each category that I want to list the related post, I created a page. These pages have the Front Matter with pagination and category data. Inside this page I include the [postsByCategory.html][postsCat-ref] created before.

{% highlight ruby %}
layout: default
title: "Algorithm Category"
permalink: /algorithm/
pagination:
  enabled: true
  category: algorithm
  permalink: /:num/
  sort_field: 'title'
  sort_reverse: false
---
{ % include postsByCategory.html % }
{% endhighlight %}

<h3>Conclusion</h3>

Here I improve my blog to the second version adding pagination and category. I had to adapt the home.html and header.html of the theme. You can see the result after the improvements.

<center>
  <img src="/img/jekyll/version2.png" width="556" height="400">
</center>

<br/>

My next step is to improve the site with the menu and other good things.

See you in the third version!!!


[markdown-ref]: https://atom.io/packages/markdown-writer
[resources-ref]: https://jekyllrb.com/resources/
[QuickStart-ref]: https://jekyllrb.com/docs/
[ruby-ref]: https://www.ruby-lang.org/en/
[ruby101-ref]: https://jekyllrb.com/docs/ruby-101/
[installation-ref]: https://jekyllrb.com/docs/installation/
[step-by-step-ref]: https://jekyllrb.com/docs/step-by-step/01-setup/
[structure-ref]: https://jekyllrb.com/docs/structure/
[varible-ref]: https://jekyllrb.com/docs/variables/
[theme-ref]: https://pages.github.com/themes/
[minima-ref]: https://github.com/jekyll/minima
[pagination-ref]: https://jekyllrb.com/docs/pagination/
[pagination-plugin-ref]: https://github.com/sverrirs/jekyll-paginate-v2
[pagination-examples-ref]: https://github.com/sverrirs/jekyll-paginate-v2/tree/master/examples
[config-file-ref]: https://github.com/sverrirs/jekyll-paginate-v2/blob/master/README-GENERATOR.md
[my-config-ref]: https://github.com/fabiana2611/fabiana2611.github.io/blob/master/_config.yml
[postsCat-ref]: https://github.com/fabiana2611/fabiana2611.github.io/blob/master/_postsByCategory.html
[index-ref]: https://github.com/fabiana2611/fabiana2611.github.io/blob/master/index.md
[nav-ref]: https://jekyllrb.com/tutorials/navigation/
[webjeda-ref]: https://blog.webjeda.com/jekyll-categories/
