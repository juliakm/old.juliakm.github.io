---
layout: post
title: "Adding author name to the Drupal search index"
date: 2008-04-01 11:04:11
category: drupal
redirect_from:
  - /adding-author-name-drupal-search-index/
---

Awhile back, I wanted to add author names to the Drupal search index. After poking around a bit, I found that this was actually pretty easy. I created a new module called custom_helper and in it put the following function: 

`
<?php
//Adding author name to the search index
function custom_helper_nodeapi($node, $op, $arg = 0) {
  switch ($op) {
    case 'update index':
      if ($node->uid) {
        $user = user_load(array('uid' => $node->uid));
        return $user->name;
      }
  }
?>
` 
One thing to keep in mind is that if you do this, then you will need to re-index all of your previously indexed nodes if you wanted them to be indexed by author name.