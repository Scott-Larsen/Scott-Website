---
layout: post
title: VSCode not finding mypy in pyenv
---

Alternatively, you can change the `Mypy: Dmypy Executable` setting, although this only works for me on the project folder settings, not `user` settings that I would think would apply to all of my settings. For this you need to get the path to mypy's daemon. In Terminal, from whichever folder/ virtual environment you're running type `which mypy`. In my case that returns `/Users/Scott/.pyenv/versions/3.9.1/envs/traversy_btre_project/bin/mypy` for my global pyenv/ python. If you haven't already, click the tab to take you to the project folder settings, not the default `user` settings and when you enter the path for the `Mypy: Dmypy Executable`, remember to append a `d` in front of `mypy` in your path. In my case that means `/Users/Scott/.pyenv/versions/3.9.1/envs/traversy_btre_project/bin/dmypy`.

Here's the full Terminal error message before I changed the settings:
