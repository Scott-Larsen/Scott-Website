---
layout: post
title: Linking to a PDF (CV / Resume) from your Jekyll Header / Nav
---


This seems like the most basic task but I finally had to resort to writing every link structure combination I could conceive of (~10, in all) and copy my *Resume.pdf* file into multiple folders to figure out how to do this.  In the end I put my *Resume.pdf* file in a folder titled *static* in my home folder.  From there I added a link to the *header.html* file amongst the list of other navigation links as follows.  The key part is that it have a leading forward slash after the baseurl - *"\{\{ site.baseurl \}\}/static/Resume.pdf"*

```
        <li class="inline-block">
          <a target="_blank" class="align-middle link-primary mr-2 mr-lg-0 ml-lg-2" href="{{ site.baseurl }}/static/Resume.pdf">Resume</a>
        </li>
```

Also of note, you may want to include *a target="_blank"* so that the PDF opens in a new tab instead of replacing your site in the browser.