---
layout: post
title: Nuxt - Google Lighthouse - noopener Breaking Links
---

I ran [Google Lighthouse](http://developers.google.com/web/tools/lighthouse) on a Nuxt site that I built and implemented their performance tuning and accessibility hints and was actually able to get 100% scores across the board (Woohoo!).  It wasn't until the next day that I realized that I had crippled all of the external links that I had on the site opening in a new tab (with ```target="_blank"```).  Lighthouse recommends always adding ```rel="noopener"``` or ```rel="noreferrer"``` to prevent the new website from manipulating the redirect elsewhere.  I dutifully searched through all my site files (thanks VSCode) for ```target="_blank"``` and replaced it with ```target="_blank" rel="noopener"```.  It turns out that was the problem and when I went back and did the same operation replacing all the ```rel="noopener"``` with ```rel="noreferrer"```, everything seems to be working again.