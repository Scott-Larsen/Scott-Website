---
layout: post
title: AttributeError Marshmallow object has no attribute SQLAlchemyAutoSchema
---

I was working on the really good (and free!) [Real Python](https://realpython.com) tutorial [Python REST APIs With Flask, Connexion, and SQLAlchemy](https://realpython.com/flask-connexion-rest-api-part-2/) and came across the following error.

```AttributeError: 'Marshmallow' object has no attribute 'SQLAlchemyAutoSchema'```

It turns out that I needed to install not only `marshmallow` but also `marshmallow-sqlalchemy`. Run the following in your terminal/ shell.

```python3 -m pip install marshmallow-sqlalchemy```

Thanks to [Art Chaz on Stack Overflow](https://stackoverflow.com/a/57984785) for the heads-up.