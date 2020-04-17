---
layout: post
title: Pyenv and Venv / Virtualenv wrapper settings
---

I've had a hell of a time wrapping my head around managing Python versions on my machine with pyenv, and individual project dependencies with venv (/ virtualenv) and an even harder time getting them to work on my (Mac) machine.  The issue I had with pyenv was finally resolved when I just moved the declaration in my `.bash_profile` from the beginning of the file to the end.  My favored way of editing it (with Nano) is done by invoking `nano ~/.bash_profile` in terminal, although I also discovered I could edit it directly in VSCode when I found the `.bash_profile` in my home (`Scott` in my case) folder (I think you have to unhide hidden files, which hides all system/ dotfiles by default).  I don't exactly understand what is happening in the code below but the reason it needs to be toward the end of `.bash_profile` is that pyenv apparently intercepts and redirects PATH listings you may have earlier in the file.

```
# PyEnv
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init -)"
fi
```

As for virtualenvwrapper, I was finally able to get that to work with the following code, modeled on this answer from [Stack Overflow](http://stackoverflow.com/questions/13242933/initializing-virtualenvwrapper-on-mac-10-6-8-for-django#13242965).  It wasn't working for me for the longest time and I think it was because I had mismatched quotation/ apostrophe/ backticks around the file locations, which I didn't discover until opening it in VSCode where it became immediately apparent visually.  In the end those marks weren't actually necessary as you can see in the code below.  It's probably obvious but the WORKON and PROJECT links are completely customizable with the WORKON folder holding all of your virtualenv folders/ files and the PROJECT folder holding a matching project folder for each virtualenv.  `$HOME` in this case designates your home folder, akin to `~/` on a Mac.

```
# virtualenvwrapper
source `which virtualenvwrapper.sh`
export WORKON_HOME=$HOME/Desktop/DATA/SORT/CodingProgrammingPython/virtualenvs
export PROJECT_HOME=$HOME/Desktop/DATA/SORT/CodingProgrammingPython
```