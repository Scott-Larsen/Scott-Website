---
layout: post
title: Python Naming Conventions (PEP 8)
---

This is an attempt at consolidating the naming conventions from [pep8.org]("pep8.org").  Please reach out if I have something wrong here as I'm just learning myself.

- *Module (File) names, Function names, Method names* and *(Instance) Variables* should all use `snake_case` (all lowercase letters, with underscores as necessary - when in doubt, use snake case).

- *Class Names* use the `CapWords` convention (no spaces, capitalize first letter of each word).

- *Constants* should use `ALL_UPPERCASE` (all uppercase letters with underscores as necessary)

- *Private elements* (available only internally) should have an `_underscore` appended in front of them.

- If you must use a reserved keyword (something that has meaning within Python), append an `underscore_` to the end of the variable (`class_`, `min_`, etc).

- Package names use `alllowercase`, without underscores.

- Never use the characters `l` (lowercase letter 'el'), `O` (uppercase letter 'oh'), or `I` (uppercase letter 'eye') as single character variable names.
