---
layout: post
title: "Drupal Theming: Create a Subpage Template that Applies to Multiple Pages on a Newspaper Site"
date: 2008-01-06 12:13:31
---

While working on a new Drupal site, I needed to set the same "subsection" template for multiple pages. The site is for an online newspaper and I wanted to use a new template for each of the section homepages. A good example of a similar approach is on CNN.com, where the [US section page][1] looks different than both the [homepage][2] and the [article pages][3]. In past projects, I've confused myself with template names. Six months later, I have trouble remembering what page-node-1432.tpl.php actually controls. So, this time, I set out to have better named template files and to have the same template file control multiple pages. So far, this has made it easier for both the project graphic designer and I. Here's the code that I put in my template.php file to make page-subsection.tpl.php the template file for node/17658, node/17638, and node/17628. `
<?php

function _phptemplate_variables($hook, $vars = array()) {
 switch ($hook) {
    case 'page':
      if((arg(0)==’node’) && ((arg(1) == ‘17658’) || (arg(1) == ‘17638’) || (arg(1) == ‘17628’))){ 
	    $vars‘template_files’ = ‘page-subsection’; 
	    }
    }
	  return $vars;
}
?>
` This code is effectively saying, if the page you are on has the node id 17658, 17638, or 17628, use the page template page-subsection.tpl.php.

 [1]: http://www.cnn.com/US/
 [2]: http://www.cnn.com/
 [3]: http://www.cnn.com/2008/US/weather/01/06/california.storm.ap/index.html