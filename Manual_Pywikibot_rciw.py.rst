.. raw:: mediawiki

   {{MoveToMediaWiki}}

 **rciw.py** is a simple IRC script to check for Recent Changes through
IRC, and to check for interwikis in those recently modified articles.

Can not be run manually/directly, but automatically by maintainer.py

In use on hu:, not sure if this scales well on a large wiki such as en:
(Depending on the edit rate, the number of IW threads could grow
continuously without ever decreasing)

Warning: experimental software, use at your own risk

Parameters
----------

-safe Does not handle the same page more than once in a session

.. raw:: mediawiki

   {{Manual:Pywikipediabot/Global Options}}

`rciw.py <Category:Pywikibot scripts>`__
