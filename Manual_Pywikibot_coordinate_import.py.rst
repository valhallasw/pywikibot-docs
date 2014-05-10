 **coordinate\_import.py** is a script to mass import coordinates from
Wikipedia to `Wikidata <Wikidata>`__.

Concept
-------

On Wikimedia wiki's Extension:GeoData is installed. This adds
coordinates to the api. This bot uses that information to add a claim to
Wikidata. By default `P625 (coordinate location) <:d:Property:P625>`__
is used. In the future the bot might support other properties as long as
the property is of type
`globe-coordinate <:d:Category:Properties with globe-coordinate-datatype>`__.

Syntax
------

The bot expects a
`generator <Manual:Pywikipediabot/pagegenerators.py>`__:

    ``python coordinate_import.py <some generator>``

`coordinate\_import.py <category:Pywikibot scripts>`__
