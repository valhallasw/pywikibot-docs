.. raw:: mediawiki

   {{languages|Manual:Pywikibot/standardize interwiki.py}}

**standardize\_interwiki.py**, this bot moves the interwiki links on top
of the articles. It is recommended to check whether this kind of bot is
accepted on your wiki. This bot should **not** be used if you are not
sure what you are doing. You should run this bot under strict
supervision because when it is launched, it will parse all articles
starting from the one you specified and will not stop :

``python standardize_interwiki.py -start "plane"``

Paramaters:

**-start** - Will ask you which page you want to start from. For
example, entering "plane", will start at "plane" and then move to the
next article starting with "pl", etc. This may flood the edits.

`standardize interwiki.py <Category:Pywikibot scripts>`__
