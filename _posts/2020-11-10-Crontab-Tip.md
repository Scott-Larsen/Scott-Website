---
layout: post
title: Crontab Secret
---

I found myself wrestling with crontab again trying to get a python script to run unsuccessfully when the most basic concept hit me. It wasn't working and I thought I was mis-configuring the numbers and asterisks, alternately setting it to run in a minute and then checking the log a minute later only to see that nothing had happened. I finally just ran the _command_ directly in the terminal. That's when I found out that the script wouldn't run because a bunch of packages were missing. I had recently switched from running it on the default (Raspberry Pi) system python which was python 2 and I needed to install all those packages again on the python 3 installation I was now calling via crontab. BTW, this was the crontab command that finally worked (and would have been working the whole time if I had the packages installed). Also new to me, the `>> /home/pi/pi-timelapse/log.txt` portion of the commmand writes the normal terminal output - which is suppressed when running via crontab - to a log file. Bottom line, try running your full command (minus the \*s and numbers [and logging]) from the terminal before getting mired by the crontab timing minutiae.

`1 4 * * * /usr/bin/python3 /home/pi/pi-timelapse/timelapse.py >> /home/pi/pi-timelapse/log.txt`

... so in this case run...

`/usr/bin/python3 /home/pi/pi-timelapse/timelapse.py`

... and work through any errors that may pop up before trying crontab.
