---
layout: post
title: "How to Move a Drupal Site to a New Host Without Going Crazy"
date: 2009-05-25 12:09:32
---

<h3 id="preparation">
  Preparation
</h3>

*A. Upgrade modules and Drupal core code*

Although it’s tempting to move your files and database quickly, I strongly recommend doing some preparation first. Before I move Drupal site, I always first check for any new Drupal core and module updates. If there are modules that need to be updated, I do the update before moving my site. The advantage of this is that it is easier later on to debug any problems that arise during the migration if you are already using the latest version of all Drupal code. 

*B. Check your version of PHP and MySQL on the new and current host*

Some Drupal modules require PHP 5.x. I’ve run into problems before when I move over code to a new server that is running PHP 4.x. 

To check your PHP version, log into your new and old servers separately via ssh and run the following:

` php -v ` 
*Helpful advice from Scor in the comments:* The PHP CLI is not always installed and php -v might not work, or if it does it might be a different version than the one Apache runs. In any case that does not mean you cannot use Drupal on the server. Another way to check these things is to try to install a dummy Drupal core site and see if it works ok. 
To check what version of MySQL you are using, open MySQL via the shell on your computer and type:

`status` 
If you are running different versions of PHP and/or MySQL on your new and old servers, be sure to check for any incompatibilities with your modules. Any module that requires PHP 5.x should say so in the README.txt document. I highly recommend making sure that your new host uses PHP 5.x before switching. 

You can also check the PHP and MySQL versions of your old site via Drupal on the status page at admin/reports/status.

<h3 id="create_your_new_domain">
  Create Your New Domain
</h3>

*C. Create your new domain at your new host*

Depending on your host, there are many ways that you could go about creating your domain. For most hosts, there will be a tool where you can define your new domain. It is important to note that creating your domain at your new host will not move your site. You will need to change your DNS records for that to happen. 

<h3 id="moving_databases">
  Moving Databases
</h3>

*D. Export your Drupal database using phpMyAdmin*

*Note:* If you do not have phpMyAdmin and are not familiar with the command-line, an alternative option is to use the [Backup and Migrate module][1]. 

If you decide to use phpMyAdmin, I recommend truncating (emptying) the cache tables before you export your database. Go to all of the tables that start with cache_ and select the "Empty" tab. You can also manually clear Views Cache within the Views module. 

To export a database using phpMyAdmin, go to the database and select the “Export” tab. I recommend checking the “Extended inserts” checkbox and saving your export as a “gzipped” file. 

*E. Create the database on your new host*

Depending on your hosting provider, there are many ways that you can go about creating a database. I recommend creating a database with the same name as the one on your old host. 

*F. Import your SQL file*

Once you have a database on your new host, you can go and import the SQL file you downloaded to your desktop using phpMyAdmin. Select your new, empty database and then click the “Import” tab. Under the “File to import” option, you can upload your file. Once the file is uploaded, you can select “Go.”

*Warning*: If you have a large site, importing your file into your new database can take a really long time. Do not stop the operation. Just wait. If your import times out, then you will need to look at importing using command-line or a program like [BigDump][2]. 

*G. Moving files*

If you are not familiar with the command-line, you can download all of your files to your desktop and then upload them to your new host using FTP. However, this process can be very slow. I recommend using secure copy (scp) instead. 

To use scp, you first need to know where your files are on your current site. Log into your old site using ssh or ftp and get the path to your web directory from the server root. Once you are in the correct directory, enter:

`pwd` 
Copy the output to somewhere you’ll be able to find again. 

Next, log into your new host and go to the directory where you want the new files to go. The following worked for me:

`scp -rp myusername@www.myoldhost.com:[/home/myusername/www.myoldhost.com/public_html]/* .` 
The part after the colon, in brackets, is the path you just copied on your old site. <u>The brackets are just here as an example, do not include them when you scp.</u>

This command copies everything in the public_html folder on my old host to the current folder of my new host. the -p flag preserves permissions and the -r flag recursively copies so that you get the content of your folders.

Be sure to check and make sure that the .htaccess file copied over as well. 

*Note:* You could also use subversion, git or another version control system to download the new files provided that you host your repository on a different site than your old host. If you are doing this, then you probably have already moved past this step. 
<h3 id="setting_up_and_testing_the_new_site">
  Setting Up and Testing the New Site
</h3>

*H: Edit Settings.php* To correctly configure your database, edit your settings.php with your new domain information. Be sure to scan through settings.php and remove any settings that you may have added that only relate to your old host. 

*I: Edit Your Hosts File*

You can test your site locally by editing your hosts file. By editing your hosts file, you will be able to see what your site looks like before making the DNS switch. 

I have a Mac and edit my hosts file in “private/etc/hosts.” To test it, I added a new line where the first column is the IP address of my new site and the second is the domain I’m testing. 

<pre>IP address of new site      www.mydomainname.com
69.123.11.11                www.juliakm.com
</pre>

The hosts file is a little trickier to find on Windows machines.This Wikipedia article gives a list of host file locations for different operating systems.</p> 
*J: Test your site locally*

Once you have your new site showing up using your hosts fix, make sure to test your new site. I recommend trying the following: 

*   Log in
*   Check your site status at admin/reports/status
*   Create a post
*   Edit an existing post
*   Post a comment
*   View your module list at admin/build/modules/list

*K: Fix any problems*

A few problems that I’ve run into before are: 

*   Not making my files/ directory writable
*   Not having the GD Library installed at my new host

For the GD Library, you’ll have to talk to your new hosting provider. For the files directory, go to the directory above your files directory and enter via command-line: 

`chmod -R 755 files` 
If you are confused about the “chmod” command, search for it on Drupal.org. There is a wealth of information available there. 

*L: Undo hosts file changes*

Go back to your hosts file and reverse any changes you made. 

*M: Set up your cron job*

Depending on your familiarity with command-line, you can do this via crontab or a tool provided by your hosting company. If your hosting company does not have a tool and you do not want to touch the command-line, check out the [Poorman’s Cron module][4]. 

<h3 id="make_the_switch">
  Make the Switch
</h3>

*N: Your last step is to switch your nameservers from your old site to new site.*

Your new hosting company should have provided you with nameservers that correspond to your new server. To point your site to these, you’ll need to go to your domain registrar and edit the DNS records. If your registrar is your old host, you can do this there. If you used another registrar such as GoDaddy, then you’ll need to edit the DNS records there. 

*O: Wait 15 minutes to 48 hours and obsessively check “whois”*

It takes awhile for DNS changes to propagate. You’ll have to wait at least 15 minutes for the change to take place. Depending on where you live in the country and your registrar, it could take even longer. You can check and see if the switch has happened by typing the following into the command-line:

`host mysite.com` 
Next, copy the IP address. Then do: 

`whois IPAddress ` 
You can also check for whois information online using [DomainTools][5]. 

<h3 id="pat_yourself_on_the_back">
  Pat Yourself on the Back
</h3>

Congratulations, you have now moved your Drupal site to a new host.

 [1]: http://drupal.org/project/backup_migrate
 [2]: http://www.ozerov.de/bigdump.php
 []: http://en.wikipedia.org/wiki/Hosts_file
 [4]: http://drupal.org/project/poormanscron
 [5]: http://www.domaintools.com