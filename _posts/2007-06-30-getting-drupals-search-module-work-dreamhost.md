---
layout: post
title: "Getting Drupal's Search Module to Work on Dreamhost"
date: 2007-06-30 19:16:50
---

One of my first frustrations with Drupal was that I could not seem to get the search module to work. I searched my new Drupal site again and again and was irked to find that each search returned the unhelpful response, "Your search yielded no results." After searching the forums, I realized out that the search module only works if you have set up a cron job on your server for cron.php. The easiest way to do this via Dreamhost is to go to the control panel (panel.dreamhost.com). Here are the steps to take once there: 1. Click on "Goodies" on the left navigation menu of your control panel. At the bottom of the new menu that just appeared, select "Crob Jobs." 2. Click "Add New Cron Job." 3. On the next screen, create a title for your cron job such as drupancron and enter the following code in the "Command to Run" box: `
wget http://www.yoursite.com/cron.php
` Make sure to replace "yoursite" with the name of your site. 4. Mark the job as "Enabled" and select how frequently your cron job should run. If you post infrequently, once a day should be sufficient. Otherwise, you should consider running the job hourly. 5. Wait an hour or a day to make sure that your cron job is running effectively by searching for a term that you know will have search results.