---
layout: post
title:  "Jekyll - Category"
date:   2019-07-17
categories: jekyll
permalink: /:categories/jekyll-category
---

This post will show you how I improve my first version of my blog. I am using Jekyll with GitHub and my first version uses the [minima theme](https://github.com/jekyll/minima) in a simple way. The second version I added category.

<center>
  <img src="/img/jekyll/version1.png" width="556" height="400">
  <em>Version 1</em>
</center>

<br/>

<h3>What is Jekyll</h3>

> Jekyll is a simple, extendable, static site generator.

The Jekyll was created with [Ruby][ruby-ref], then, to use that you'll need to have the Ruby in your machine. The first step you can see [here][QuickStart-ref]. The menu on the right side there is two important links ([Ruby101][ruby101-ref] and [Installation][installation-ref]) that will help you on your configuration.  You don't need to be an expert in ruby because the site will give you enough information.

After that, you will find many [resources][resources-ref] such as plugins and editors That you can to add to make easier your work. The editor that I am using is the [markdown][markdown-ref] because I am using the atom to work on my blog.

<h3>Main Concepts</h3>

[**Liquid**](https://jekyllrb.com/docs/step-by-step/02-liquid/) is the first concept. It is a templating language that you permit you to manipulate object, tags and filters on the pages.

[**Front matter**](https://jekyllrb.com/docs/front-matter/) is such a config header of your page. You have to have this to indicate the title, category, date, any variable that you need.

Also you can have [**layout**](https://jekyllrb.com/docs/step-by-step/01-setup/), [**include**](https://jekyllrb.com/docs/step-by-step/05-includes/) tag, [**data files**](https://jekyllrb.com/docs/step-by-step/06-data-files/) (CSV, JSON, etc), [**assets**](https://jekyllrb.com/docs/step-by-step/07-assets/) (CSS, images, js), [**blogging**](https://jekyllrb.com/docs/step-by-step/08-blogging/) (list of posts) and [**Collections**](https://jekyllrb.com/docs/step-by-step/09-collections/).

The posts have to be inside of the \_post folder, each post must have **front matter** and the names' post must have a filename with the publish date, a title, and an extension. It's a great practice is to use categories to organize the posts.

The detail about these components you will find on [Step by Step][step-by-step-ref].

Another important concept is the [directory structure][structure-ref] with folder and pages organization. When you use Ruby, you create a project that is build all the structure for you. The reserved folder will start with '\_'. When you use a theme and want to customize this you need to follow the same structure.

Moreover, exist [variables][varible-ref] that are very helpful to manipulate the data from your blog. The scope can be global, site or page.

And the last but not least, if you want to use a theme, Jekyll has many options, but to use in GitHub there are just a few numbers of [theme possible][theme-ref].

The theme that I'm using in my blog until the moment of this post is [minima][minima-ref].

<h3>Category Menu</h3>

Show posts by category is an important point in a blog. To do this, I got examples from [navigation doc][nav-ref] and [webjeda][webjeda-ref].

The first step that I did was create a category menu (categoryMenu.html) and the [postsByCategory.html][includesFolder-ref] file such a complementary code to filter by category.

Inside the [header.hml][includesFolder-ref] file from the theme I changed the main menu to be static and added the category menu.

To list by category, I create a [page by category][categoryfolder-ref] and include the fragment [postsByCategory.html][includesFolder-ref] inside them. The loop just use variables to manipulate the categories.

{% highlight ruby %}
{% include postsByCategory.html categoryName=site.categories.algorithm %}
{% endhighlight %}

<h3>Conclusion</h3>

In this post, I improve my blog to the second version adding the categories. I had to adapt the [header.html][includesFolder-ref] of the theme but it is usual if you want to customize the theme.

Be free to customize your theme. If you would like to see another post that is using jekyll on github and give detail on how to do that you can see [here](https://glens.site/how-I-created-this-blog).

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
[includesFolder-ref]: https://github.com/fabiana2611/fabiana2611.github.io/tree/master/_includes
[index-ref]: https://github.com/fabiana2611/fabiana2611.github.io/blob/master/index.md
[nav-ref]: https://jekyllrb.com/tutorials/navigation/
[webjeda-ref]: https://blog.webjeda.com/jekyll-categories/
[categoryfolder-ref]: https://github.com/fabiana2611/fabiana2611.github.io/blob/master/category
