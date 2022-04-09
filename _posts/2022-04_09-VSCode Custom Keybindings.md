---
layout: post
title: Samsung TV Remote Code
exclude: true
---

I was having trouble syncing my VSCode settings accross different installations and it was caused, at least partially, because I forgot to add a comma between the first and second entries below. I thought I would share these, both to help others and to help future me. The first allows me to execute an open Python script by typing `cmd` and `b`. The next two allow me to uppercase or lowercase highlighted text by typing `cmd`, `shift` and `u` or `l`, depending on what I want to do. You can edit it within VSCode by clicking `cmd`, `shift`, `p` and searching for `Shortcuts (JSON)`. The `JSON` is important because the other `Keyboard Shortcuts` is just a list of every keyboard shortcut built into VSCode. This code is stored in a file named `keybindings.json` in `~/Library/Application Support/Code/User` on my Mac so you could probably edit it directly there.

```
// Place your key bindings in this file to override the defaultsauto[]
[
    {
        "key": "cmd+b",
        "command": "python.execInTerminal"
    },
    {
       "key": "cmd+shift+u",
       "command": "editor.action.transformToUppercase",
       "when": "editorTextFocus"
    },
    {
       "key": "cmd+shift+l",
       "command": "editor.action.transformToLowercase",
       "when": "editorTextFocus"
    }
   ]
```
