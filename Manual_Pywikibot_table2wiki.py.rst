.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/table2wiki.py}}

.. raw:: mediawiki

   {{MoveToMediaWiki}}

 **Table2wiki.py** is part of the `Pywikipedia
bot <Using the python wikipediabot>`__ framework.

Converts HTML-tables to MediaWiki's language.

Examples
--------

Example of the simplest syntax:

    table2wiki.py "article name"

In this example, only 1 article is changed.

The process can also take place automatically, to do this a xml dump is
needed:

``table2wiki.py -xml:20050406_cur_table.xml -lang:en ``

-xml = name of the xml dump.

Note: Every change needs to be checked. This bot can make mistakes.

`table2wiki.py <Category:Pywikibot scripts>`__
