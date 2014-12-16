---
layout: post
title: "How to Decide Between Using Taxonomy Terms and a CCK Field to Classify Content on a Drupal Site"
date: 2009-03-19 13:29:29
---

I often have a hard time deciding whether to use a <span class="caps"><span class="caps">CCK</span></span> field or the <a class="zem_slink" href="http://en.wikipedia.org/wiki/Taxonomy" title="Taxonomy" rel="wikipedia">taxonomy</a> module when building <a class="zem_slink" href="http://drupal.org" title="Drupal" rel="homepage">Drupal</a> sites. At Drupalcon, I was glad to see that I am not alone in my confusion. At the Drupalcon Drupal Taxonomy Revisted session, I finally started to understand the use case for each.

Here’s a table I put together to help me quickly decide whether to use taxonomy or <span class="caps"><span class="caps">CCK</span></span> in the future.

<table>
  <tbody>
    <tr>
      <th>
        Question
      </th>
      
      <th>
        Which to Use?
      </th>
      
      <th>
        Rationale
      </th>
    </tr>
    
    <tr>
      <td>
        Do you have a lot of terms or attributes?
      </td>
      
      <td>
        As the size of your <a class="zem_slink" href="http://en.wikipedia.org/wiki/Vocabulary" title="Vocabulary" rel="wikipedia">vocabulary</a> or field option list grows, taxonomy becomes a better choice
      </td>
      
      <td>
        CCK stores its values as text while taxonomy stores values with an ID. This makes lookups over a large data set more efficient for taxonomy.
      </td>
    </tr>
    
    <tr>
      <td>
        Are you using a hierarchy?
      </td>
      
      <td>
        Taxonomy
      </td>
      
      <td>
        Taxonomy is designed to handle multiple levels of hierarchy, which a <span class="caps"><span class="caps">CCK</span></span> field is not
      </td>
    </tr>
    
    <tr>
      <td>
        Are you listing attributes? For example, listing the color options of a car.
      </td>
      
      <td>
        CCK
      </td>
      
      <td>
        CCK makes more sense if you have created a content type and are adding attributes to it using <span class="caps"><span class="caps">CCK</span></span> fields. For example, I could have a car node type and color would be a <span class="caps"><span class="caps">CCK</span></span> field
      </td>
    </tr>
    
    <tr>
      <td>
        Does your piece of content exist in the real world on its own?
      </td>
      
      <td>
        Taxonomy
      </td>
      
      <td>
        Taxonomy terms are designed to map to real-world objects in a way that <span class="caps"><span class="caps">CCK</span></span> fields are not. For example, if I have a taxonomy of US States, each state exists whether or not I have assigned content to it.
      </td>
    </tr>
    
    <tr>
      <td>
        Will you re-use your term or attribute in multiple ways within your site or re-organize them?
      </td>
      
      <td>
        Taxonomy
      </td>
      
      <td>
        If you have a classification such as US States that you plan to use in multiple node types, then taxonomy makes more sense. It is easier to add new terms to taxonomies over time than to individual <span class="caps"><span class="caps">CCK</span></span> fields.
      </td>
    </tr>
    
    <tr>
      <td>
        Are you using <span class="caps"><span class="caps">CCK</span></span> or taxonomy to list critical information on your site? What is the cost of losing the data if you upgrade to a future major Drupal version?
      </td>
      
      <td>
        Taxonomy
      </td>
      
      <td>
        Taxonomy is more futureproof because each term has its own unique id, and, it can be moved between vocabularies. Taxonomy is also a Drupal core module and there will almost certainly be an easy upgrade path from Drupal 6 taxonomy to Drupal 7 taxonomy.
      </td>
    </tr>
  </tbody>
</table>

### An Example: Classifying Topic Areas

Using this criteria, making the decisions I was [stuck on in an earlier blog post][1] becomes a lot easier. 

 [1]: http://www.juliakm.com/paging-niklp-deciding-between-cck-fields-and-taxonomy

<table>
  <tbody>
    <tr>
      <th>
        Question
      </th>
      
      <th>
        Response
      </th>
      
      <th>
        Decision
      </th>
    </tr>
    
    <tr>
      <td>
        Do you have a lot of terms or attributes?
      </td>
      
      <td>
        Yes, we have at least 200 terms and that number is likely to grow dramatically over the next few years.
      </td>
      
      <td>
        Taxonomy
      </td>
    </tr>
    
    <tr>
      <td>
        Are you using a hierarchy?
      </td>
      
      <td>
        Yes, we have at least 3 levels of hierarchy.
      </td>
      
      <td>
        Taxonomy
      </td>
    </tr>
    
    <tr>
      <td>
        Are you listing attributes? For example, listing the color options of a car.
      </td>
      
      <td>
        No, we are listing topics that span multiple content types.
      </td>
      
      <td>
        Taxonomy
      </td>
    </tr>
    
    <tr>
      <td>
        Does your piece of content exist in the real world on its own?
      </td>
      
      <td>
        Somewhat. Greenhouse Gas Inventories exist in the real-world, as does the “Climate.” The category “Campus Operations” is more of a grey area
      </td>
      
      <td>
        Probably Taxonomy
      </td>
    </tr>
    
    <tr>
      <td>
        Will you re-use your term or attribute in multiple ways within your site or re-organize them?
      </td>
      
      <td>
        Yes, we plan to classify many different node types with the same terms
      </td>
      
      <td>
        Taxonomy
      </td>
    </tr>
    
    <tr>
      <td>
        Are you using <span class="caps"><span class="caps">CCK</span></span> or taxonomy to list critical information on your site? What is the cost of losing the data if you upgrade to a future major Drupal version?
      </td>
      
      <td>
        It would be painful to lose all of our classification information but I don’t think that it would destroy us as an organization.
      </td>
      
      <td>
        CCK or Taxonomy
      </td>
    </tr>
  </tbody>
</table>

After evaluating which to use with my new handy chart, it’s clear the taxonomy makes more sense for classifying our topical areas.

<div style="margin-top: 10px; height: 15px;" class="zemanta-pixie">
  <a class="zemanta-pixie-a" href="http://reblog.zemanta.com/zemified/ac85ab0e-dd1c-4623-bb1a-310acd93b65b/" title="Zemified by Zemanta"><img style="border: medium none ; float: right;" class="zemanta-pixie-img" src="http://img.zemanta.com/reblog_e.png?x-id=ac85ab0e-dd1c-4623-bb1a-310acd93b65b" alt="Reblog this post [with Zemanta]" /></a><span class="zem-script more-related"></span>
</div>