 **illustrate\_wikidata.py** is a script to add images to Wikidata
items.

Concept
-------

On Wikimedia wiki's Extension:PageImages is installed. This adds a new
page property "page\_image". This bot uses that information to add a
claim to Wikidata. By default `P18 (image) <:d:Property:P18>`__ is used,
but it's also possible to add other properties as long as the property
is of type
`commonsMedia <:d:Category:Properties with commonsMedia-datatype>`__.

Syntax
------

The bot expects a
`generator <Manual:Pywikipediabot/pagegenerators.py>`__:

    ``python illustrate_wikidata.py <some generator>``

You can change the property to be add. For example to add `P41 (flag
image) <:d:Property:P41>`__:

    ``python illustrate_wikidata.py -property:P41 <some generator>``

`newitem.py <category:Pywikibot scripts>`__
