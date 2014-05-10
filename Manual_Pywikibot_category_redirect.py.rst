.. raw:: mediawiki

   {{MoveToMediaWiki}}

**category\_redirect.py** will move pages out of redirected categories.

The bot will look for categories that are marked with a category
redirect template, take the first parameter of the template as the
target of the redirect, and move all pages and subcategories of the
category there. It also changes hard redirects into soft redirects, and
fixes double redirects. A log is written under
``&lt;userpage>/category_redirect_log``. Only category pages that
haven't been edited for a certain cooldown period (currently 7 days) are
taken into account.

Parameters
----------

No bot-specific parameters.

.. raw:: mediawiki

   {{Manual:Pywikibot/Global Options}}

`category redirect.py <Category:Pywikibot scripts>`__
