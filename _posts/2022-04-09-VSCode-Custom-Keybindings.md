---
layout: post
title: VSCode Custom Keybindings
---

I was having trouble syncing my VSCode settings across different installations and it was caused, at least partially, by the fact that I forgot to add a comma between the first and second entries below. I thought I would share these, both to help others and to help future me. The first allows me to execute an open Python script by typing `cmd` and `b`. The next two allow me to uppercase or lowercase highlighted text by typing `cmd`, `shift` and `u` or `l`, depending on what I want to do. You can edit it within VSCode by clicking `cmd`, `shift`, `p` and searching for `Shortcuts (JSON)`. The `JSON` is important because the other `Keyboard Shortcuts` is just a list of every keyboard shortcut built into VSCode. This code is stored in a file named `keybindings.json` in `~/Library/Application Support/Code/User` on my Mac so you could probably edit it directly there, too.

<script src="https://gist.github.com/Scott-Larsen/80cd40a77ce0b56ed100b37d5f1012bc.js"></script>

VS Code - Visual Studio Code
