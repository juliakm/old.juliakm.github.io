---
layout: post
title: "Exploring Drupal One Module at a Time"
date: 2007-06-24 21:56:20
---

Although Wordpress has served me well, I decided that it might be fun to try and rebuild my site using Drupal. For the most part, switching has been easy. I started off with a version on my local computer using MAMP and then transitioned to my Dreamhost account. Dreamhost's databases are slow running Wordpress, and seem to be just as slow running Drupal. But, I didn't expect a speedier site with Drupal. After playing around with 

[Zen][1], I decided to start with the [Foundation theme][2]. I was to reproduce my old Wordpress design in about 4 hours. That theme was a very modified version of [Skuteczni][3]. The hardest part of figuring out Drupal was knowing what modules to install. When I first installed Wordpress, I found that I could put together a decent blog without having to install a bunch of plugins. With Drupal, doing almost anything requires a module. The advantage of this is that the core Drupal download is quite small. The disadvantage is that figuring out what modules to install requires quite a bit of searching the forums. Additionally, one of the strange features of Drupal is that the modules that come with your first installation are not all enabled. The core installation is divided into required and optional modules. However, a lot of the typical "blog" features are in the optional modules. For example, you need to turn on the Aggregator module to generate RSS feeds. In addition to enabling a number of optional modules (Blog, Comment, Menu, Path, and Search), I downloaded a bunch of modules. One of the first modules I downloaded was wp2drupal, which I would not recommend using. The wp2drupal module is designed to copy Wordpress posts into your Drupal site. Although I eventually got this module working, in the process I ran into a number of blank screens. From what I read on the forums, it seems like wp2drupal is designed for Drupal 4.7 and that getting it to work on Drupal 5 is not a seamless process. I also downloaded CCK and Views. CCK lets you define your own content types and is a fantastic resource. Views is useful for creating specific lists such as a list of most recent posts. I am sure that Views does much more, but I have not fully delved into it yet. I haven't added any Views to my site yet, but I plan to later on. One of my frustrations while installing Drupal was that I could not seem to get rid of the "Julia's Blog" link at the bottom of each blog post. After searching through the documentation, it seemed like I had three options. I could hide the text with CSS, modify the core code, or, change the nodetype of my content from blog to story. I decided to change the node type using the very helpful [nodetype module][4]. My last step in setting up my site was to learn about and implement Drupal SEO best practices. I found [a couple][5] [good posts][6] on the topic and downloaded the [pathauto][7], [search404][8], [nodewords][9], [page_title][9], and [gsitemap][10] modules. In the next couple of weeks, I hope to get the site search to work more effectively and to add some cool Views. I will try to post notes on my progress.

 [1]: http://drupal.org/project/zen
 [2]: http://drupal.org/project/foundation
 [3]: http://www.headsetoptions.org/
 [4]: http://drupal.org/project/nodetype
 [5]: http://blamcast.net/articles/drupal-seo
 [6]: http://devbee.com/drupal_seo
 [7]: http://drupal.org/project/pathauto
 [8]: http://drupal.org/project/search404
 [9]: http://drupal.org/project/nodewords
 [10]: http://drupal.org/project/gsitemap