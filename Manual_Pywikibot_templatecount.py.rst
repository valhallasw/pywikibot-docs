.. raw:: mediawiki

   {{svn/pywikipedia}}

.. raw:: mediawiki

   {{Pywikibot|script}}

As the name implies **templatecount.py** counts the number of times a
template has been transcluded on your wiki.

Syntax
------

Basic syntax is:

    ``python templatecount.py ''option'' templatename1 templatename2 templatename3 ... templatenameX``

where ``''option''`` can be

::

    -count        Counts the number of times each template (passed in as an
                  argument) is transcluded.

    -list         Gives the list of all of the pages transcluding the templates
                  (rather than just counting them).

    -namespace:   Filters the search to a given namespace.  If this is specified
                  multiple times it will search all given namespaces

Usage
-----

Imagine you wanted to find out how often the templates , and were used
on your wiki, across all namespaces. You didn't care about *where* they
were used, just *how many times*. You'd then type:

    ``python templatecount.py -count reflist quote tl``

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/templatecount.py}}

`templatecount.py <Category:Pywikibot scripts>`__
