---
layout: post
title: Storing JSON 'File' in Heroku Config Vars
---

It seems like a problem ripe for <vomet>*disruption*</vomet> but for a junior dev who still doesn't know best practices around storing private API keys I think I came up with a clever workaround for this thorny situation.  The problem is that I was trying to deploy to Heroku a ([Flask / Python site](ww-rsvp.heroku.com)) that writes to a Google Sheet and therefore needs OAuth authentication.  Heroku has "Config Vars" in which you can store a private key that won't be accessible to the public and you can keep out of your Git/ GitHub/ source control.  The problem in this case is that OAuth gives you a JSON file of about 8 values, at least two of which are needed for authentication, if not more.  The solution seemed obvious - to store that JSON as text in a Config Var but implementation proved anything but easy for me.  After more than a day of fiddling, I think I finally have it working.

Store the JSON file locally in your project folder, in my case I called it ```client_secret.JSON```, and immediately add it to your .gitignore file to make sure it doesn't get tracked/ uploaded to source control.  Next you have to 'clean' the JSON of special characters because Python's json module didn't like many of the 'special characters' that were included.  This doesn't need to be done for the actual JSON file stored locally but it will be necessary for what you upload to Heroku.  You might make a new Python file in order to verify that it's clean, in which case, open it with ```import json``` and below that assign the text of your JSON to a variable (in my case ```client_secret```) as a multiline string (use three apostrophes before and after the string).  Below that you want to run it through ```json.loads``` which in my case looks like the following.

client_secret = json.loads(client_secret)

From there you have to clean the string "JSON" to get rid of all of the newline characters and tabs/ spaces that broke the ```'private key'``` up into digestible lines.  This takes it from ~10 shortish lines of code to one absurdly long one.  Next, at the beginning and end of the private key, delete the ```-----BEGIN PRIVATE KEY-----``` and ```-----END PRIVATE KEY-----```.  The dashes in this trips up the json module.  I'm not sure what else, if anything, had to be done but the beauty is you can run that short Python script and it will tell you the location of any other characters it's choking on.  Fix those and then it's on to the next step.

Now you can put that "JSON" string in a Heroku Config Var by issuing the following commands in terminal with your variable name of choice before the equals sign and your absurdly long multiline string (without the parantheses) after it.

```heroku config:set *client_secret*=*YourReallyLongStringOfJSON*```

To then pull the credentials down from the Config Var into your main Python file, insert code similar to this.  

```import os

client_secret = os.environ.get('client_secret') # This pulls your variable out of Config Var and makes it accessible
if client_secret == None: # This is to detect if you're working locally and the Config Var isn't accessible
    print('\n\nResorted to local JSON file.\n\n') # so it pulls from the locally stored JSON file.
    with open('client_secret.json') as json_file:
        client_secret = json.load(json_file)```

After pasting that code I actually thought I had to convert the string back to JSON within my program and that it wouldn't work but it looks as though that's unnecessary.  If you know of a better way to solve this issue, please let me know because this seems kludgy but I couldn't find anything better when I Googled.  The beauty of this is that, so long as you set up your ```gitignore``` file properly you should be able to upload the project to GitHub without exposing your private keys.