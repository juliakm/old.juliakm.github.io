---
layout: post
title: "Displaying Nodeprofile Fields for a User within a Node"
date: 2008-02-03 11:49:33
---

I was banging my head against the wall this weekend trying to remember how to display nodeprofile fields with user information. It's actually really easy and I thought I should write a post about how to do it for the next time I forget. In this case, I have a content type called 'myuserprofile' that is selected as the content type to use for nodeprofiles. In my myuserprofile content type, I have a field for users to enter their favorite food. There are two easy ways of displaying this information. First, we can grab and display it within a node. For example, say that I want to display a user's favorite food on a page if that user is logged in. To do so, the following would work: 

`<?php
global $user;
//checking if a user is logged in
if ($user->uid):
//load the nodeprofile user profile for the currently logged-in user
$profile = node_load(array('type'=>'myuserprofile', 'uid'=>$user->uid));
//print out the user's favorite food
print $profile->field_favorite_food[0]['value'];
?>
` A second approach to displaying this information, is to put the following in the \_phptemplate\_variables function of template.php. 

`
<?php 
function _phptemplate_variables($hook, $vars = array()) {
switch ($hook) {
    case 'node':
      //checking if a user is logged in
	if ($user->uid):
	
		$vars['profile'] = node_load(array('type'=>'myuserprofile', 'uid'=>$user->uid));
		$vars['favorite_food'] = $vars['profile']->field_favorite_food[0]['value'];
	endif;
	break;
    }
    return $vars;
}
?>
` Then, I can display the favorite food information on a page with: 

`
<?php 
global $user;
print $favorite_food;
?>

`