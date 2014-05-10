 `watchlist.py <category:Pywikibot scripts>`__ **watchlist.py** merely
outputs the watchlist of the account running the script.

Syntax
------

Syntax is straightforward, as there appear to be no arguments which can
be used with it. Just type

::

    python watchlist.py

Usage
-----

From a command line this displays the currently logged in account's
watchlist as a list of page titles, and updates the local cache of the
watchlist used by other pywikipediabot modules.

When calling from other programmes, useful functions within this module
include *refresh()* (refreshing the local copy of the watchlist,
normally only done monthly) and *isWatched()* (returning True or False)
with *watch()* and *unwatch()* available from *wikipedia.py*.

For example the following Python code will unwatch any matching
currently watched image on Commons category "Flowers":

.. code:: python

    import wikipedia, catlib, pagegenerators
    from watchlist import isWatched

    site = wikipedia.getSite('commons', 'commons')
    cat = catlib.Category(site,u'Category:Flowers')
    gen = pagegenerators.CategorizedPageGenerator(cat,recurse=False)

    for page in gen:
      title=page.title()
      if isWatched(title, site):
        print "Unwatching",title
        page.unwatch()

