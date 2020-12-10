---
layout: post
title: Screen Recording with FFMPEG
---

I've been toying with recording some coding sessions - like Advent of Code problems - and so needed to figure out a way to record my screen.  I've been using ffmpeg for two other recent projects and suspected it was capable because it seems to be able to do everything.  Getting it going was somewhat straightforward although getting it to output timestamped filenames (to avoid overwriting) took me a few hours to iron out.  What I suspect will work for most people is the following.

`ffmpeg -f avfoundation -r 30 -s 1440x900 -i "1:1" -f segment -strftime 1 -segment_time 10:00:00 "screenRecording%Y-%m-%d_%H-%M-%S.mkv"`

Be sure to swap out your screen's resolution (replace `1440x900` as necessary) and the `"1:1"` indicates which 'input' device to consume (You can get the available devices by running `ffmpeg -f avfoundation -list_devices true -i ""`.)  I've got some demon on my older Macbook Pro that makes the built-in webcam unavailable unless I've restarted recently so I actually have to run it as `"0:0"`.  

On some machines the `-strftime` may work as intended but it took me hours to find the solution that I had to add the `-f segment` ... `-segment_time 10:00:00` in and amongst the `-strftime` command to get it to do the timestamp replacement.  The `segment` command apparently breaks the recording up in segments but if you just set it for a time longer than what you're intending to record - 10 hours in this case - it should get the `-strftime` functionality to work properly.