---
layout: post
title: Removing Hidden Blog Post Links from Next Previous
---

I have a few posts on my (Jekyll) blog that aren't related to tech that I have hidden from the main blog page (although they're available by search or direct URL). There are several blog posts showing you how to accomplish that functionality so I won't get into it. What I didn't realize until recently was that they were still showing up in the Next / Previous links at the bottom of other posts. The blog posts that should be excluded have `exclude: true` within their front matter (header) so from there it was a matter of extending the same usage of `unless` from the main blog page to the code that linked to the Next / Previous posts.

Here are the important code snippets:

<script src="https://gist.github.com/Scott-Larsen/ff9fcdd529f43a646b301c88e219cba8.js"></script>

and this is the full code:

<script src="https://gist.github.com/Scott-Larsen/b84ed75d95d3e9829a1829ba23af8a68.js"></script>
