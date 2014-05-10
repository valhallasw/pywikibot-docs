.. raw:: mediawiki

   {{MoveToMediaWiki}}

This bot cleans `Commons:Category:Non-empty category
redirects <Commons:Category:Non-empty category redirects>`__ by moving
all the files, pages and categories from redirected category, which were
not edited for at least a week, to the target category.

The bot will look for categories that are marked with a category
redirect template, take the first parameter of the template as the
target of the redirect, and move all pages and subcategories of the
category there. Only category pages that haven't been edited for a
certain cooldown period (currently 7 days) are taken into account, to
prevent edit wars and vandalism.

Parameters
----------

No bot-specific parameters.

.. raw:: mediawiki

   {{Manual:Pywikibot/Global Options}}

`commons category redirect.py <Category:Pywikibot scripts>`__
