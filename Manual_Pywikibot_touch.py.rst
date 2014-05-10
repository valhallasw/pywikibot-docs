.. raw:: mediawiki

   {{MoveToMediaWiki}}

When a page needs to be changed in order to refresh all kinds of
relations, **touch.py** can do the work. This program updates a record
without making any changes. Running **touchall.py** will not create
entries on the "recent changes". Technically, what it does is take each
page and save it, without making any changes (`null
edit <m:Help:Null_edit>`__), thus refreshing the relations with
categories and other relations.

Scenario 1
----------

When a category is added to a much used template, running touch.py will
add the existing pages to the category.

Parameters
----------

    **start:** The default is to go through all pages from
    Special:Allpages in order. This may however be done spread out over
    various runs. If one wants to continue, give the argument
    "-start:page!" with page the last page of which you know it has been
    done. The bot will then do the pages coming after that.

Touch also understands the `general
parameters <Manual:Pywikibot/Global_Options>`__ '-lang' and '-family'.

``touch.py -start:!``

See also
--------

-  `Using the python wikipediabot <Using the python wikipediabot>`__

`touch.py <category:Pywikibot scripts>`__
