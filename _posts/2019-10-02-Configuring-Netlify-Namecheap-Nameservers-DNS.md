---
layout: post
title: Configuring Namecheap Nameservers (DNS) for a Netlify deployment of a Nuxt Site
---


Log in to your account with Namecheap and click on **Account** at the top right of the screen if your domain name isn't already listed on screen.

![Main Screen, click on Account.]({{ site.baseurl }}/images/Screen-Shot-2019-10-03-at-9.15.43-PM.jpg)




Click on the **Manage** button to the right of the domain you hope to redirect.
\
\
![Click on Manage]({{ site.baseurl }}/images/Screen-Shot-2019-10-03-at-9.16.45-PM.jpg)

\

Click the **Advanced DNS** button on the top right tab.

![Go to Host Records]({{ site.baseurl }}/images/Screen-Shot-2019-10-03-at-9.18.51-PM.jpg)

\

Look for the **Host Records** which may be any combination of A Record, CName Record, Alias Record, URL Redirect Record, etc.

![Set and Alias Record]({{ site.baseurl }}/images/Screen-Shot-2019-10-03-at-9.19.50-PM.jpg)

I hesitate to tell you to delete any but you need to set an Alias Record with the host being an @ symbol, the Value is your Netlify address for your app (in my case *nostalgic-torvalds-afe855.netlify.com* [it seems to add the trailing period after I save it]) and TTL to Automatic.  To make sure any request going to your domain name including www you need a second record, a URL Redirection Record with a host of www, your domain name (in my case *http://lindadove.net* [without the www]) and Unmasked selected.

You may have to wait up to 20 minutes for the changes to take effect and remember to do a hard refresh (Command-Shift-R on a Mac) or check the site in a Private/ Incognito window so you aren't getting a cached old version.  Let me know if this doesn't work for you or if you have improvements.  Your next best bet is to go directly to Namecheap's support chat.
