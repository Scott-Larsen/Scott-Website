---
layout: post
title: Cron Test Script
---

I recently upgraded my MacOS version and my cron jobs stopped running. It ended up being a file access permission issue but in the process I realized I didn't have a good method to test whether cron was running. All of my cron jobs are background processes so, in addition to having to change the times that they run, I'd also have to dig into my system to see if they ran successfully. I figured that someone else would've written a short script to test whether cron is running but a quick Google search came up empty. So here's the basic Python script I came up with that I'm sharing in the hopes of saving others a few minutes time. This will create a directory in whichever folder you set in `DESTINATION_FOLDER` named with the current date and time as such - `!cron_test_17-05-2021_12-48-41`.

```python
import os
from datetime import datetime

DESTINATION_FOLDER = "/Users/Scott/Downloads/"  # Include trailing path seperator

now = datetime.now()
foldername = now.strftime("!cron_test_%d-%m-%Y_%H-%M-%S")

os.mkdir(DESTINATION_FOLDER + foldername)
```
