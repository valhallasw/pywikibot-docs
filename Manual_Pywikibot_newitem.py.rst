 **newitem.py** is a script to mass create new `Wikidata <Wikidata>`__
items.

Concept
-------

New articles get created all the time on Wikipedia. With this script you
can create new items connected to these articles. The bot looks at the
age of the page and the last edit to the article. If both exceed the
minimum threshold, the new item will be created. The default thresholds
is 21 days for article creation and 7 days since last edit.

Syntax
------

The bot expects a
`generator <Manual:Pywikipediabot/pagegenerators.py>`__:

    ``python newitem.py <some generator>``

You can modify the thresholds. This is the number of days. For example
minimum age of 7 days and not edited for 2 days:

    ``python newitem.py -pageage:7 -lastedit:2 <some generator>``

`newitem.py <category:Pywikibot scripts>`__
