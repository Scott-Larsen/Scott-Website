---
layout: post
title: Removing Hidden Blog Post Links from Next Previous
---

I have a few posts on my (Jekyll) blog that aren't related to tech that I have hidden from the main blog page (although they're available by search or direct URL). There are several blog posts showing you how to accomplish that functionality so I won't get into it. What I didn't realize until recently was that they were still showing up in the Next / Previous links at the bottom of other posts. The blog posts that should be excluded have `exclude: true` within their front matter (header) so from there it was a matter of extending the same usage of `unless` from the main blog page to the code that linked to the Next / Previous posts. My site won't rebuild if I put in the code snippet but you want to have `if page.previous.url` ... `unless page.previous.exclude`.

The full code:

```
<!-- Use if you want to show previous and next for all posts. -->
{% assign user_url = site.url | append: site.baseurl %} {% assign full_base_url
= user_url | default: site.github.url %} {% if page.previous.url %} {% unless
page.previous.exclude %}
<div class="col-4 sm-width-full left mr-lg-4 mt-3">
  <a
    class="no-underline border-top-thin py-1 block"
    href="{{ page.previous.url | prepend: full_base_url }}"
  >
    <span class="h5 bold text-accent">Previous</span>
    <p class="bold h3 link-primary mb-1">{{ page.previous.title }}</p>
    <p>{{ page.previous.content | strip_html | truncatewords:20 }}</p>
  </a>
</div>
{% endunless %} {% endif %} {% if page.next.url %} {% unless page.next.exclude
%}
<div class="col-4 sm-width-full left mt-3">
  <a
    class="no-underline border-top-thin py-1 block"
    href="{{ page.next.url | prepend: full_base_url }}"
  >
    <span class="h5 bold text-accent">Next</span>
    <p class="bold h3 link-primary mb-1">{{ page.next.title }}</p>
    <p>{{ page.next.content | strip_html | truncatewords:20 }}</p>
  </a>
</div>
{% endunless %} {% endif %}
```
