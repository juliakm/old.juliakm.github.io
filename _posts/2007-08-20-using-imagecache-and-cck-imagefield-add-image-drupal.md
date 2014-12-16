---
layout: post
title: "Using Imagecache and CCK Imagefield to Add an Image in Drupal"
date: 2007-08-20 20:11:17
category: drupal
redirect_from:
  - /using-imagecache-and-cck-imagefield-add-image-drupal/
---

Figuring out how to get Drupal's [imagecache module][1] to work with [CCK's imagefield][2] can about as fun as a trip to the dentist. Although I found a lot of articles analyzing the benefits of using Image vs. CCK imagefield, I could not find one source with clear instructions on how to implement imagefield with imagecache. So, here's my stab at an explanation of how to get imagecache to work with imagefield.

 [1]: http://drupal.org/project/imagecache
 [2]: http://drupal.org/project/imagefield

1. Install and activate CCK, imagefield, and imagecache. Go to Admin > Content types and select the content type that you want to add an image field to. Click on "Add field" to add an image field. Then, give your field a title, select Image and create your field. The name of my field is "related_images."

<img src="/resources/u1/createfield.png" alt="create cck image field" height="205" width="278" /> 
2. Set your imagecache presets at Site Building > Image cache. My preset is has the namespace "homepage" and is set to resize with a width and height of 100. 

<img src="/resources/u1/namespace.png" alt="drupal preset namespace" height="321" width="500" /> 
3. Go back to the content type that you added a CCK image to by selecting Content Management > Content types. Click on the name of the content type you previously added an image to. In the content type's menu, select "Display fields."

<img src="/resources/u1/displayfields.png" alt="display cck image fields" height="94" width="415" /> 
4. Look to the right of the listing for the image field you created. Set the teaser and body to the namespace you set in step 2. My namespace is "homepage." 

<img src="/resources/u1/chooselook.png" alt="set display of cck image" height="66" width="500" /> 
5. Add a new article of content using the content type that has your new image field. Upload an image as part of the post and make sure that your image displays at the width and height you set in "Display fields."

6. If you want to have your image display in a template such as node.tpl.php, the following code will print the image and image title for a CCK image field called field\_related\_images: 

`
<?php print $node->field_related_images[0]['view']; ?> 


<?php print $node->field_related_images[0]['title'];  ?>
`