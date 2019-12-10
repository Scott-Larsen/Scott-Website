---
layout: post
title: Jekyll CSS Not Rendering
---

I had a problem with this here Jekyll install/ blog in that I couldn't get the CSS to render and nearly abandoned Jekyll because it was the third major issue I'd encountered in the few short weeks of trying to get it going.  Thankfully a guy named Gungor on the [Jekyll Gitter forum](http://gitter.im/jekyll/jekyll) pointed out to me that my css was being served at ```http``` while my site was at ```https``` (It's possible that I have those reversed).  I spent the next three hours trying to figure out what I needed to change and, after trying every iteration of ```http/s``` in the ```url``` and ```baseurl``` variables in my ```_config.yml``` file, I finally commented them both out and it suddenly worked.  I wish I could explain why but if you're running Jekyll on GitHub Pages with a custom domain see if that doesn't fix your problem.