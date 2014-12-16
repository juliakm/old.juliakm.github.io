---
layout: post
title: "Drupal Permissions Issues: A Debugging Checklist"
date: 2008-01-12 15:15:24
---

Every once in awhile, when working on a Drupal site, my content either disappears or I cannot log-in. At this point, I usually get rather angry and start thinking of worse case scenarios. What if I can never log into my site again? What if anonymous users can't read articles? In a rare moment of clarity, I put together the following Drupal permissions debugging checklist. I hope that you find it as useful as I have. 

**1. Check user access control and make sure that all users can "access content"** *Path:* mysite.com/admin/user/access Often, when installing a module, I accidentally change key permissions. For example, a couple of times I have allowed anonymous users to "access content" but not logged-in ones. Although my access control permissions are usually not the problem, its always best to check them before moving onto the next approaches. 

**2. Check input filter roles** *Path:* mysite.com/admin/settings/filters One problem with having a lot of input filters is that you can easily mess up the permissions of a particular filter. If a user does not have permission to use an input filter, then they cannot edit content that can only be edited with that input filter. To give a real-world example, say that I set up a new input filter called "tinyMCE." Next, I set up my permissions for tinyMCE so that only my webmaster role can use the tinyMCE input filter. While doing this, I also set permissions so that only the webmaster can use my "Filtered HTML" and "Full HTML" input filters. Next, I set up a new role called "intern" and let the intern edit content. However, my intern reports that he cannot access any of the edit pages. Why? He needs to have access to the "tinyMCE" input filter. 

**3. Clear site cache and views cache** *Path for Views Cache:* mysite.com/admin/build/views/tools Sometimes site cache and views cache can result in strange permissions problem. Site cache can be reset with the Developer module "Empty cache" menu option. To have this appear, you need to enable the Devel block. In addition to clearing the site cache, sometimes it helps to clear the ciews cache. This is especially true if your permissions problems started after you edited a view. The option to clear views cache can be found in the Tools section of the ciews administration page. 

**4. If all else fails, rebuild node permissions** *Path:* mysite.com/admin/content/node-settings/rebuild Sometimes Drupal node permissions get corrupted. When this happens, rebuilding the node permissions can solve the problem. Please be advised that if you have a lot of nodes, this can take a very long time. 

**5. The Last Step: Looking for Module-Specific Issues** *Path for Update Script:* mysite.com/update.php If none of the previous steps work, I usually try to figure out if the problem is caused by a module that I just installed. First, if I recently installed a new version of a module, I make sure that I have run the update.php script. Next, I generally disable the module, and then repeat step three. 

**6. The Bonus Step: Backtrace** *Backtrace Module:* http://drupal.org/project/trace Sebastien Hinderer wrote in to suggest using PHP's backtrace function as an additional debugging tool. You can use the [Trace module][1] and/or the [debug\_print\_backtrace() PHP function][2]. Using backtrace, you can identify which Drupal function triggered an "Access Denied" message and save lots of debugging time. Please let me know if there are other ways of hunting down and fixing permissions issues that you know about.

 [1]: http://drupal.org/project/trace
 [2]: http://php.net/manual/en/function.debug-print-backtrace.php