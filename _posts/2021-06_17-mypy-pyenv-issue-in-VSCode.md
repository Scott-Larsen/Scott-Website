---
layout: post
title: VSCode not finding mypy in pyenv
---

I kept getting an error message when trying to save Python files in VSCode and it had something to do with pyenv and mypy.

Googling turned up nothing relevant so I just had to poke around. To be honest, I'm still not perfectly clear on the issue but it seems that the default settings of mypy weren't pointed to the mypy daemon (dmypy) installed in my pyenv installations/ shims. In VScode, I went to `Code > Preferences > Extensions` and searched for `mypy`.

![Main Screen, click on Account.]({{ site.baseurl }}/images/Screen Shot 2021-06-17 at 12.58.22 PM.png)

From there I clicked the gear icon and selected `Extension Settings`.

![Main Screen, click on Account.]({{ site.baseurl }}/images/Screen Shot 2021-06-17 at 12.58.33 PM.png)

I clicked the checkbox that says `Mypy: Run Using Active Interpreter` and that seems to resolve the issue (You might get a warning to install mypy at that point).

![Main Screen, click on Account.]({{ site.baseurl }}/images/Screen Shot 2021-06-17 at 1.54.09 PM.png)

Alternatively, you can change the `Mypy: Dmypy Executable` setting, although this only works for me on the project folder settings, not `user` settings that I would think would apply to all of my settings. For this you need to get the path to mypy's daemon. In Terminal, from whichever folder/ virtual environment you're running type `which mypy`. In my case that returns `/Users/Scott/.pyenv/versions/3.9.1/envs/traversy_btre_project/bin/mypy` for my global pyenv/ python. If you haven't already, click the tab to take you to the project folder settings, not the default `user` settings and when you enter the path for the `Mypy: Dmypy Executable`, remember to append a `d` in front of `mypy` in your path. In my case that means `/Users/Scott/.pyenv/versions/3.9.1/envs/traversy_btre_project/bin/dmypy`.

Here's the full Terminal error message before I changed the settings:

```
[22] Error running mypy in /Users/Scott/Desktop/DATA/SORT/CodingProgrammingPython/traversy_btre_project: mypy failed with error: "pyenv: dmypy: command not found". See Output panel for details.
Document saved: /Users/Scott/Desktop/DATA/SORT/CodingProgrammingPython/traversy_btre_project/btre/settings.py
[23] Check workspace: /Users/Scott/Desktop/DATA/SORT/CodingProgrammingPython/traversy_btre_project
[23] Received python path from Python extension: /Users/Scott/.pyenv/versions/3.9.1/envs/traversy_btre_project/bin/python
[23] Running dmypy in folder /Users/Scott/Desktop/DATA/SORT/CodingProgrammingPython/traversy_btre_project
/Users/Scott/.pyenv/shims/dmypy --status-file '/Users/Scott/Library/Application Support/Code/User/workspaceStorage/0b5d5df9c8fb7d5b31262bb092c70e03/matangover.mypy/dmypy-3bc5a742efe88c8e510ad328c3fbedd5ea9383c3.json' run --log-file '/Users/Scott/Library/Application Support/Code/User/workspaceStorage/0b5d5df9c8fb7d5b31262bb092c70e03/matangover.mypy/dmypy-3bc5a742efe88c8e510ad328c3fbedd5ea9383c3.log' -- . --show-column-numbers --no-error-summary --no-pretty --no-color-output --python-executable /Users/Scott/.pyenv/versions/3.9.1/envs/traversy_btre_project/bin/python
[23] stderr:
pyenv: dmypy: command not found

The `dmypy' command exists in these Python versions:
  3.9.1/envs/oreilly_beyond_basic_programming
  3.9.1/envs/oreilly_complete_python
  3.9.1/envs/oreilly_python_survival_skills
  3.9.1/envs/traversy_btre_project
  oreilly_beyond_basic_programming
  oreilly_complete_python
  oreilly_python_survival_skills
  traversy_btre_project

Note: See 'pyenv help global' for tips on allowing both
      python2 and python3 to be found.

[23] Error running mypy in /Users/Scott/Desktop/DATA/SORT/CodingProgrammingPython/traversy_btre_project: mypy failed with error: "pyenv: dmypy: command not found". See Output panel for details.
```
