---
layout: post
title: "GMailThis for Google Apps"
date: 2009-02-22 11:10:35
---

I recently tried to set up the really useful GMailThis! bookmarklet for a Google Apps email site and found that I had to slightly change the code to get it working. The original Javascript is at http://contrapants.org/blog/2005/07/gmailthis.html. Here it is: 

`
<a href="javascript:popw='';Q='';x=document;y=window;if(x.selection) {Q=x.selection.createRange().text;} else if (y.getSelection) 
{Q=y.getSelection();} else if (x.getSelection) {Q=x.getSelection();}popw = y.open('https://mail.google.com/mail?view=cm&
tf=0&to=&su=' + escape(document.title) + '&body=' + escape(Q) + escape('\n') + 
escape(location.href),'gmailForm','scrollbars=yes,width=680,height=510,top=175,left=75,status=no,resizable=yes');if (!document.all)
 T = setTimeout('popw.focus()',50);void(0);">GmailThis!</a> 
` For my Google App, I had to change the line **https://mail.google.com/mail** to **http://mail.google.com/a/mysite.org/mail/**. Here's a working bookmarklet for a site anexample.org. `
<a href="javascript:popw='';Q='';x=document;y=window;if(x.selection) {Q=x.selection.createRange().text;} else if (y.getSelection)
 {Q=y.getSelection();} else if (x.getSelection) {Q=x.getSelection();}popw = y.open('http://mail.google.com/a/anexample.org
/mail/?view=cm&fs=1&tf=1&to=&su=' + escape(document.title) + '&body=' + escape(Q) + escape('\n') + escape(location.href) + 
'&zx=RANDOMCRAP&shva=1&disablechatbrowsercheck=1&
ui=1','gmailForm','scrollbars=yes,width=680,height=510,top=175,left=75,status=no,resizable=yes');if (!document.all) T = 
setTimeout('popw.focus()',50);void(0);">GmailThis!</a>
`