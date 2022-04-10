---
layout: post
title: RegEx for Finding Open and Closing Tags in HTML
---

TLDR for `<li>` `</li>`:

`<[/\n\r]*li[^>]*>`

I'm web scraping with Python and BeautifulSoup on some very _unconventional_ code and I needed to find out how nested a set of unordered lists is. I would think that VSCode has a way of tracking opening and closing HTML tags but I wasn't seeing it (Let me know if there's a method or plugin that I'm missing). The next best thing I could think of was to use a regex to search. I haven't had much practice with Regular Expressions but was able to piece this query together from several Stack Overflow answers and the documentation.

To search for an opening list tag is a straightforward...

`<li>`

If you want opening `<li>` and closing `</li>` tags you need...

`<[/]*li>` (the star ignores anything in the preceding square brackets)

And since some tags have more information like `<li class="some-class">` you need to add...

`<[/]*li[^>]*>`

I'll be totally honest about this last addition `[^>]*`. My best understanding is that it's essentially a double-negative. It's saying match everything `^` except the greater-than `>` symbol and then the asterisk `*` after the square brackets tells you to ignore everything you've found other than that closing `>`.

And finally, since some of the opening `<li>` tags in the code I was searching extended over multiple lines I had to add `\n` newline characters and return characters `\r` as other characters to ignore upfront.

So the final code ends up being....

`<[/\n\r]*li[^>]*>`

Happy Searching!
