 **claimit.py** is a script to mass add `Wikidata <Wikidata>`__ claims
to a lot of items based on pages on Wikipedia

Concept
-------

A category or template on Wikipedia gives information about what kind of
page it is. For example if it contains a person infobox, it's probably a
person. Or as another example: If a page is in a certain taxonomic
family category, it's probably in that family. Based on this information
you can instruct the bot to add
`claims <:d:Wikidata:Glossary#Claims_and_Statements>`__.

Syntax
------

The bot expects a
`generator <Manual:Pywikipediabot/pagegenerators.py>`__ and a pairs of
`property <:d:Wikidata:List of properties>`__ and
`item <:d:Wikidata:Glossary#Entities,_Items,_Properties_and_Queries>`__:

    python claimit.py P1 Q2 P3 Q4

`claimit.py <category:Pywikibot scripts>`__
