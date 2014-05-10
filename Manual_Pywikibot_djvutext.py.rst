.. raw:: mediawiki

   {{MoveToMediaWiki}}

 **djvutext.py** extracts the ocr text from a djvu page image and
uploads it to the corresponding page in the page namespace on
Wikisource. In order for the bot to function, a djvu file must be in the
same folder pywikipediabot runs from and it must be identical to the
djvu used for the index file on Wikisource.

On a blank page this script will leave a blank page and set the
pagequality level=0 (without text) and the user= to the name of your bot
(e.g. ).

Parameters
----------

The following parameters are supported:

| ``   -dry           If given, doesn't do any real changes, but only shows``
| ``                  what would have been changed.``
| ``   -ask           Ask for confirmation before uploading each page.``
| ``                  (Default: ask when overwriting pages)``
| ``   -djvu:...      Filename of the local djvu file (i.e. in your PWB folder)``
| ``   -index:...     Name of the index page on Wikisource``
| ``                  (Default: the djvu filename)``
| ``   -pages:``\ \ ``-``\ \ `` Page range to upload; ``\ \ `` is optional (e.g. "-pages:1-" will upload all pages)``

All other parameters will be regarded as part of the title of a single
page, and the bot will only work on that single page.

`djvutext.py <Category:Pywikibot scripts>`__
