---
layout: post
title: Install Python Packages from within an iPython Session
---

TIL that you can install python packages from within an iPython session by appending an `!` to the front of your normal command. Say you're 20 commands deep into a tutorial and the instructor neglected to mention that you'd need numpy, seaborn and matplotlib. Just enter....

`!python3 -m pip install numpy seaborn matplolib`

This doesn't seem to work in my regular bash terminal on Mac so let me know if you know the trick for that.
