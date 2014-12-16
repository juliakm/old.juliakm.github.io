---
layout: post
title: "Paging NikLP: Deciding between CCK Fields and Taxonomy"
date: 2008-10-16 19:38:42
---

I'm trying to decide between using a CCK field or taxonomy to classify content on a new site. We plan to have various node types (video, podcasts, forum topics, news articles, courses, etc.) and want to be able to dynamically pull together all nodes with the same tag in a page. There will be dynamic pages for both universities and topics. The topics will have a hierarchy. For example:

Campus Operations (located at www.mysite.com/topic/campus-operations) — Climate (located at www.mysite.com/topic/campus-operations/climate) ——Greenhouse Gas Inventories (located at www.mysite.com/topic/campus-operations/climate/greenhouse-gas-inventories)

As detailed above, Campus Operations, Climate, and Greenhouse Gas Inventories should each have their own page. I would also be able to see that Greenhouse Gas Inventories has the parent page Climate and that its parent is Campus Operations. [Here’s a very rough example topic page][1] and a [university one][2]. I would also like to be able to associate one page with multiple parents. For example, Greenhouse Gas Inventories may also have a parent page of Campus Inventories. Additionally, it should be easy to generate a dynamic listing of topics in their hierarchy with links to the topic pages. 

 [1]: /resources/rc_topicpage.pdf
 [2]: /resources/rc_schoolpage.pdf

If associating topic pages with more than one parent page is too difficult, then changing parent topics should at least be easy to change. For example, I might want to change the tag Greenhouse Gas Inventories to GHG Inventories and then have all of the content with the old tag now be tagged with the new term. Using CCK fields, I’ve had problems with this in the past. 

If I use a taxonomy, I'll probably wind up with at least 4 levels.

Topic A —Topic AB ——-Topic ABC ———-Topic ABCD

It needs to be easy for administrators to add new topics sub-topics. We may also want to let users tag content. However, I can imagine that a potential user may take one look at our complex taxonomy and run for the hills. I understand that one option for presenting taxonomy to users may be to use something like [Content Taxonomy][3] and make the interface simpler. 

 [3]: http://drupal.org/project/content_taxonomy

To add even more complexity, I need to be able to make some taxonomy terms only visible to specific roles. 

In summary, here are my requirements for topics: - Classify many node types in a hierarchical list with a minimum of four levels - Dynamically generate pages for some but not all terms (most likely using Views). The pages should have a specific layout. - It should be easy for users to tag new content - Administrators need to be able to edit the terms without causing problems later on - Some dynamically-generated pages should only be visible to users with specific roles

<h3 id="and_there8217s_more8230">
  And there’s more…
</h3>

In addition to a topic taxonomy, I will need to build a taxonomy (or CCK field) for universities. Ideally, I would be able to easily pull all universities in California with greenhouse gas inventories. I’m thinking that the best approach for this will be to have a either a cck nodereference field for universities where each university has a node or a taxonomy of U.S. universities broken out by location. If I went with a nodereference field, then the university nodes would have to have a location cck field. 

The goal would be to easily generate links like this: www.mysite.com/schools/california/campus-operations/climate/greenhouse-gas-inventory

I think that this can be achieved by views, but I don’t want to overlook any ways of structuring the data that will make for easier querying later on. 

Here are a few articles that have added to my confusion: http://www.darcynorman.net/2008/04/24/complex-hierarchical-taxonomies-in-drupal/ http://www.johnandcailin.com/blog/cailin/drupal-cck-vs-taxonomy

It seems like I have a few options:

1) Create Multiple CCK fields or CCK fields for each level of my topic hierarchy and also have a cck nodereference field for universities. 

**Advantages:** - CCK fields can be hidden or shown for different node types, which is easier for end users to understand.

**Disadvantages:** - Even if I use hierarchical select CCK fields, CCK doesn’t have the built in advantages of taxonomy. Displaying breadcrumbs won’t be as easy, there is not a set of API functions ready to be called. 

2) Have a taxonomy for topics and also use a taxonomy for universities broken down by location. 

**Advantages:** - Taxonomies can easily handle the 4-level hierarchy

**Disadvantages:** - Commits to using taxonomy/term link structure (not sure about this) - Taxonomies may seem overly complex to end users - Long-term it might not make sense to classify universities by location. Some schools have multiple location. 

3) Have a taxonomy for topics and use a cck nodereference field for universities.

**Advantages:** - Taxonomies can easily handle the 4-level hierarchy

**Disadvantages:** - Requires creating a node for each university. Some of these nodes will have very little data. - Taxonomies may seem overly complex to end users

4) Have a taxonomy for topics, a cck field for universities, and a field for school location

**Advantages:** - Lets me pull information by location that doesn’t necessarily relate to a school

**Disadvantages** - It could be cumbersome to associate universities and locations later on - Taxonomies may seem overly complex to end users

<h3 id="conclusion">
  Conclusion
</h3>

I think that it makes the most sense to use a taxonomy for the topics and a nodereference field for universities. In the university node, there will be a field for location. This will require creating approximately 4,000 university nodes, which may lead to performance problems later on.