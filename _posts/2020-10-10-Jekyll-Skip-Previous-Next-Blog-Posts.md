---
layout: post
title: Jekyll: Skipping Next / Previous Off-Topic Blog Posts
---

I have a few posts on my (Jekyll) blog that aren't related to tech that I have hidden from the main blog page (although they're available by search or direct URL). There are several blog posts showing you how to accomplish that functionality so I won't get into it. What I didn't realize until recently was that they were still showing up in the Next / Previous links at the bottom of other posts. The blog posts that should be excluded have `exclude: true` within their front matter (header) so from there it was a matter of extending the same usage of `unless` from the main blog page to the code that linked to the Next / Previous posts `{% unless page.previous.exclude %}`.

In my case it took a little sleuthing because that code didn't exist within my local repo and didn't seem to be standard within Jekyll. I finally realized it was in the [Swiss]("https://github.com/broccolini/swiss") theme I was using. When you want to overwrite some functionality of a theme, copy over the file to be altered in a commenserate folder within your local repo. So in my case I had to copy the [previous-next.html]("https://github.com/broccolini/swiss/blob/cbf02071aff32c59030a55b0dadbe450eefa4aa3/_includes/previous-next.html") to my local `_includes` folder in order to make the change. One of the two relevant code blocks is below with the `unless` tag added at the end (and a matching `endunless`). Now you also have to do the same for the `next` portion with `page.next.exclude`.

```
{% assign user_url = site.url | append: site.baseurl %}
{% assign full_base_url = user_url | default: site.github.url %}
{% if page.previous.url %}
{% unless page.previous.exclude %}

Rest of the code

{% endunless %} {% endif %}
```
