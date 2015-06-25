---
layout: post
title: Building Drupal Forums at AASHE
date: {}
category: drupal
redirect_from: 
  - "/building-drupal-forums-aashe/"
published: true
---


The idea of building a Campus Sustainability Forum has been kicking around [my organization][1] for years. When the organization was choosing a CMS about three years ago, one of the major reasons we went with Drupal was the forum integration. 

The goal of the [AASHE Campus Sustainability Forums][2] is to provide a central place where those interested in campus sustainability can ask and answer questions, share knowledge and expertise, and contribute to the growing body of knowledge on campus sustainability.

Currently, most information about campus sustainability is exchanged via the [Green Schools Listserv][3]. While this listserv is an excellent way of quickly asking questions and getting responses, there was no one location where all of the discussion is archived and easily searched. Our goal in building the Campus Sustainability Forums was to fill this void. 

Before we started work on the forums, my co-workers scoured other web forums around the web and came back with a number of features requests from other forums. While the core Forum module met some of these requests, I found myself looking for additional modules to achieve most of the forum functionality. Here's an overview of how I used the core module and contributed modules to build the forums. 

<h2 id="core_forum_module_functionality">
  Core Forum Module Functionality
</h2>

*Create forum posts and Respond to forum posts via comments*<br /> 
Using the core Forum module, users with different permission levels are able to create posts and respond to posts with comments. Forum topics are a node type and all users are able to create forum topics. However, as explained later, only specific roles can automatically publish their topics.

*Mark posts as sticky*<br />
We wanted to be able to highlight more relevant or timely topics by having them stick to the top of topic listing pages. This is easily achieved by marking a post as sticky. In fact, this is one of the few times when I have been able to easily explain to end users what the sticky checkbox means. 

*Organize posts by taxonomy*<br /> 
AASHE has an existing classification for campus sustainability that is used within the site and is based on the [Sustainability Tracking And Reporting System (STARS)][4]. We were able to easily create a Forum vocabulary with these terms. I used the helpful [Taxonomy CSV][5] and [Taxonomy XML][6] modules to export and import taxonomies between our development, staging, and live sites. One problem that we ran into was having a forum that could be organized by multiple taxonomies, which was an initial requirement. Although you can assign new taxonomies to forum topic posts, the forum itself can only be organized by one vocabulary. This is a limitation that I wasn’t able to get around. 

*RSS feed for each forum*<br /> 
Since the forum is organized by taxonomy terms, there is an automatic RSS feed for each forum. Having separate RSS Feeds was one of our earliest requirements because someone interested in the Curriculum forum is not necessarily interested in the Waste one. One slight problem we’ve run into is that our users don’t expect the RSS icon to be for a different set of posts when you are on a taxonomy page. We are going to add some help text to further explain this later on. 

*Anonymous block to encourage users to sign-in*<br /> 
When we first tested the forum, we noticed that users were confused about how to sign in from the forums main page. To get around this, I created a block only shown to anonymous users encouraging logging in. 

*Individual topic areas can be co-branded with partner associations. For example, the ACUPCC sponsors the [Climate Forum][7]*<br /> 
While there’s no section-sponsor setup out of the box with the forum module, it was relatively easy to use blocks that appear only on particular pages to set up forum sponsors. For example, the ACUPCC sponsors our Climate forum and this sponsorship is recognized in a block. In a future version of the forum, it would be ideal to attach forum sponsors to taxonomy terms as an additional field. This should be possible in Drupal 7. 

<h2 id="adding_contributed_modules">
  Adding Contributed Modules
</h2>

*Look and feel can be customized to match main AASHE website*<br /> 
Once I started designing the forum, I quickly found that it was challenging to make the look-and-feel of the forum match the AASHE website. However, the [Advanced Forum][8] module provides a number of presets themes that make theming a lot easier. I used the Naked theme and was able to create a forum design in a few hours. 

*Ability for users to sign up for email notification (by email or RSS) of replies*<br /> 
While the RSS functionality is taken care of by the core forum module, email subscriptions were more complicated to implement. I ended up using the [Notifications][9] module, [Token][10] module, [Messaging][11], and [Mimemail][12]. Notifications and Messaging made it easy to create templates that are sent out in response to certain events such as a new comment being posted. Users are automatically sent HTML emails (using Mimemail) and can subscribe by taxonomy term, author name, content type, and thread to email notifications. However, we’ve had a bit of difficulty communicating this functionality to our users. 

*Sponsors recognized in random order on the main forums page*<br /> 
To make sure that our forum had an active base of users, we sought out sponsors. In exchange for promoting the forums, sponsor logos are presented in random order on the right side of the page and listed in text alphabetically at the bottom of each forum page. This is all accomplished using [Views][13], [Imagecache][14], [Link][15], [FileField][16] and [ImageField][17]. I set up a sponsor node type where users can enter the sponsor name, a link to the sponsor website, and upload an image that is resized to 125 pixels wide. The list of sponsor images on the right is a Views block that displays in random order and the text list on the bottom of the page is a different Views block. 

*AASHE staff logo to accompany staff posts, AASHE member logo accompanies member posts*<br /> 
We were able to easily use the [User Badges][18] module to create logos to accompany member and staff posts. The goal of this is to draw attention to “official” answers in the forum and to also highlight our members. 

*When non-members submit posts, they are not published and the AASHE moderators receive an automatic notification.*<br /> 
It has been hard to figure out how to best moderate forum posts and avoid having the forum overrun with spam and posts that violate our terms of use. Our current solution is to post any content from members without review but save as draft any posts from non-members. To accomplish this, I set up a rule using the [Rules module][19] that emails a notification to our staff moderator when we have a new non-member post or comment and also sets it as a draft. In the future, I am going to write a module that assigns all .edu email addresses a role and that role can automatically post to the forum without review. 

*The “Real Name” and not the username should show up everywhere for users*<br /> 
We don’t ever use usernames on the AASHE website and instead override all names using the RealName module. Without any modifications, the [RealName module][20] replaced all of our usernames (set with theme_username) with our profile First + Last name combination. 

*Users can “quote” one another in forum threads*<br /> 
One features that our staff really liked on other forums was the ability to quote other posts. Using the [Quote module][21], we were able to add this button and functionality. However, since Quote doesn’t use theme_username, we had to write a [small patch][22] to the module. 

*Display recent posts categorized by relevant taxonomy term throughout the site* <br />  
We wanted to be able to have relevant posts show up depending on where a user is within our site. For example, if they are looking at a Climate resource, they would see relevant Climate posts in a list block. This was implemented on our development site using Views and arguments. However, it is not implemented on the live site yet. 

<h2 id="deploying">Deploying</h2>

One of the trickiest parts of deploying our forum was that so much of the functionality was tied up in contributed modules and database code. I ended up using the Features module to bundle together the required modules, Views, content types, and imagecache presets from development to staging to live site. Feature alone didn’t capture all of the settings, so I also practiced my live migration by first moving from our development to staging site and writing down all of the little configuration settings and then using that list to move to the live site. Please let me know if you are interested in having a copy of the feature. 

<h2 id="how_it_all_came_together">
  How It All Came Together
</h2>

In the first screenshot, you can see the anonymous user block on the left, as well as a sponsor/description block. On the right, you can see our sponsor view that presents a list of logos and an example of real names being used in the last post listing. 

[<img src="http://farm3.static.flickr.com/2446/4089714778_919a0c105c.jpg" width="500" height="334" alt="AASHE Forum Homepage" />][23] 
In the second screenshot, you can see an example of member badges, our recent posts view, the subscription option and the ability to quote posts. 

[<img src="http://farm3.static.flickr.com/2620/4089714562_a549b774c0.jpg" width="500" height="328" alt="AASHE Forum Topic Page" />][24] 
## So, How Long Did It Take?
I probably spent between 50 and 60 hours building the forums and my co-worker Matt worked 5 to 10 hours. A significant amount of my time was spent trying out and then discarding modules that didn't quite meet our needs. It also took awhile to figure out how to configure Mimemail with Notifications.

 [1]: http://www.aashe.org "AASHE"
 [2]: http://www.aashe.org/forums "AASHE Forums"
 [3]: http://listserv.brown.edu/?A0=GRNSCH-L
 [4]: http://www.aashe.org/stars
 [5]: http://drupal.org/project/taxonomy_csv
 [6]: http://drupal.org/project/taxonomy_xml
 [7]: http://www.aashe.org/forums/climate
 [8]: http://drupal.org/project/advanced_forum
 [9]: http://drupal.org/project/notifications
 [10]: http://drupal.org/project/token
 [11]: http://drupal.org/project/messaging
 [12]: http://drupal.org/project/mimemail
 [13]: http://drupal.org/project/views
 [14]: http://drupal.org/project/imagecache
 [15]: http://drupal.org/project/link
 [16]: http://drupal.org/project/filefield
 [17]: http://drupal.org/project/imagefield
 [18]: http://drupal.org/project/user_badges
 [19]: http://drupal.org/project/rules
 [20]: http://drupal.org/project/realname
 [21]: http://drupal.org/project/quote
 [22]: http://drupal.org/node/364871%23comment-2129570
 [23]: http://www.flickr.com/photos/juliakm/4089714778/ "AASHE Forum Homepage by jkullama, on Flickr"
 [24]: http://www.flickr.com/photos/juliakm/4089714562/ "AASHE Forum Topic Page by jkullama, on Flickr"
