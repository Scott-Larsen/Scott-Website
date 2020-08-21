---
layout: post
title: Text Encoding TLDR
---

Here's my probably wrong and definitely incomplete takeaway on text encoding.  Instead of copy pasting decode / encode snippets from Stack Overflow I promise to get to the bottom of the encoding of the next text I scrape or import into Python.

# First there was *ASCII*
It only had 128 characters and is only really useful for typing English (non-accented, 'Latin Alphabet') text (in green text on a black screen).  There were several expansions that were largely localized for other languages but it wasn't until the invention of...

# *Unicode* made it possible to type all of the world's languages
...and then some (Klingon, apparently).  It also made it possible to add emoji 🎉.  The complication is that they came up with a few ways to compress `unicode` and so...

# *UTF-8* is the current gold standard
UTF-8 is the best implementation of Unicode.  Sort of a *square is a rectangle but a rectangle isn't a square*-type situation

To get the real story behind encoding, watch [Ned Batchelder's great talk from Pycon 2012](https://www.youtube.com/watch?v=sgHbC6udIqc&feature=emb_logo) ([Slides here](https://nedbatchelder.com/text/unipain.html)).  And for *THE* definitive article on the subject, head to [Joel Spolsky's blog post](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/) about it.  And if I've said anything incorrect, please correct me, I don't want to put bad information out into the world.