 **harvest\_template.py** is a script to mass add
`Wikidata <Wikidata>`__ claims based on information harvested from
Wikipedia templates.

Concept
-------

Templates on Wikipedia, especially `infoboxes <:w:Help:Infobox>`__,
contain a lot of useful information that can be used to add
`claims <:d:Wikidata:Glossary#Claims_and_Statements>`__ to Wikidata
`items <:d:Wikidata:Glossary#Entities,_Items,_Properties_and_Queries>`__.

Syntax
------

The bot expects a
`generator <Manual:Pywikipediabot/pagegenerators.py>`__, the name of the
template and pairs the field in the template and the
`property <:d:Wikidata:List of properties>`__ to store this in:

    ``python harvest_template.py <some generator> -template:<name of template> <field A> P1 <field B> P3``

    ``python harvest_template.py -lang:nl -cat:Sisoridae -template:"Taxobox straalvinnige" -namespace:0 orde P70 familie P71 geslacht P74``

The bot will automatically figure out whether to parse an item property
or to use a string property.

Depending on your configuration, you may need to specify which site to
pull the template from. You can do this with
``-lang:XX -family:wikipedia`` where XX is the language code of the wiki
you want to use.

`harvest template.py <category:Pywikibot scripts>`__
