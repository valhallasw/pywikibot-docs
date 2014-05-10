.. raw:: mediawiki

   {{Pywikipediabot}}

This page explains how to run python bots on `Wikidata <m:Wikidata>`__
using the basic pywikibot library.

Configuration
-------------

To start contributing/testing using your bot's account you must add the
following to your
`user-config.py <Manual:Pywikipediabot/user-config.py>`__:

production site
~~~~~~~~~~~~~~~

.. code:: python

    usernames['wikidata']['wikidata'] = u'YourBot'

testing site
~~~~~~~~~~~~

.. code:: python

    usernames['wikidata']['test'] = u'YourBot'

Working with pywikibot/compat (former *trunk release*)
------------------------------------------------------

Creating a DataPage object
~~~~~~~~~~~~~~~~~~~~~~~~~~

Different ways to create a DataPage and Page object for Wikidata: First
way is creating a data\_repo first, use this way only when you have ID
of the item (Q####)

.. code:: python

    import pywikibot
    # create a site object, here for en-wiki
    site = pywikibot.getSite('en')

    # get the data repository site for the given site
    repo = site.data_repository()

    # OR you may also get the site by language code/family:
    # repo = pywikibot.getSite('wikidata', 'wikidata')

    # We also can create a DataPage by its ID in two ways
    # First by site and title:
    data = pywikibot.DataPage(repo, "Q42")
    #OR the second way by the ID number:
    data = pywikibot.DataPage(42)

the second way is:

.. code:: python

    import pywikibot
    # create a site object, here for en-wiki
    site = pywikibot.getSite('en')

    # create a Page object for en-wiki
    page = pywikibot.Page(site, "Helium")

    # Now we create the corresponding DataPage:
    data = pywikibot.DataPage(page)
    # Warning: This page does not have a valid title until you get its content

REMEMBER: You cannot change any item, value, or label without getting
data first

Getting data
~~~~~~~~~~~~

Get the data in a simple way

.. code:: python

    # get an entity of that page
    dictionary = data.get()

    # get interwiki links as page objects
    language_links = data.interwiki()

Changing labels
~~~~~~~~~~~~~~~

.. code:: python

    data.setitem(summary=u"BOT SUMMARY",
             items={'type': u'item', 'label': 'fa', 'value': 'هلیم'})

Changing descriptions
~~~~~~~~~~~~~~~~~~~~~

.. code:: python

    page.setitem(summary=u"BOT SUMMARY",
             items={'type': u'description', 'language': 'en', 'value': 'noble gas'})

Changing sitelinks
~~~~~~~~~~~~~~~~~~

.. code:: python

    data.setitem(summary=u"BOT SUMMARY",
             items={'type': u'sitelink', 'site': 'de', 'title': 'OK'})

Changing or creating claims/statements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: python

    data.editclaim(property, value ,refs={("ref1","value1"),("ref2","value2")})

    property can be a string like "capital" or "p36" or "P36" or "36" or
    36
    value can be a string like "Moscow" or "Q649" or "q649" or "649" or
    649
    refs is optional and if you don't add any references the bot will
    change either:

        ref1 can be a string like "imported from" or "p143" or etc
        value1 can be a string like "English Wikipedia" or "q328" or etc
        other refs are optional too

Remember:\ **Important**:language of values must the same as the
Wikipedia page you load at first. For example, if you load Russia from
Deutsch Wikipedia your values must be:

.. code:: python

    data.editclaim("Hauptstadt", "Moskau" ,refs={("Datenvorlage","Englischsprachige Wikipedia ")})

and if you run your bot on English values, the bot won't work

If there was a claim already the code changes the claim, and if not the
code adds the claim.

Getting all entities (of an item)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: python

    dictionary = data.get()

Removing claim or claims
~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: python

    data.removeclaim(property, value)

you can add the property in the way shown above, value is optional and
it's better to use when we have multiple claims for a statement if you
don't use value, every claim that uses the property will be removed

Creating an item
~~~~~~~~~~~~~~~~

.. code:: python

    data.createitem('summary')

Example
-------

Simple example for creating new items.

**Caution:** Use this code snippet with care. It does not test whether a
data repository item already exists. It only test whether it exists for
a given site page. This could also mean that a given site page has no
language link on a given repository page. This should be checked before
a page is created.

.. code:: python

    # -*- coding: utf-8  -*-
    import wikipedia
    site = wikipedia.getSite('fa') # add parameter fam='wikipedia' if you haven't declared family = 'wikipedia' in your user-config.py

    list_of_articles=[u"دهستان جونقان", u"قنات_بزل_وار", u"قنات_بسک", u"قنات_بشرآباد"]
    for name in list_of_articles:
        # create a Page object of a site
        page = wikipedia.Page(site, name)
        # create the corresponding data repository object
        data = wikipedia.DataPage(page)
        if data.exists():
            wikipedia.output(u"%s already exists. Skipping..." % name)
        else:
            wikipedia.output(u"%s is missing. Creating..." % name)
            data.createitem(u"Bot: Importing article from Persian wikipedia")

Working with pywikibot/core (former *rewrite branch*)
-----------------------------------------------------

***see `d:Wikidata:Creating a bot <d:Wikidata:Creating a bot>`__*** for
an extended documentation. pywikibot core supports most Wikibase
features already, e.g., qualifiers, sources, properties with item,
coordinate, time, and string type.

.. code:: python

    import pwb #only needed if you haven't installed the framework as side-package
    import pywikibot
    site = pywikibot.Site('en','wikipedia') #  any site will work, this is just an example
    page = pywikibot.Page(site, 'Douglas Adams')
    item = pywikibot.ItemPage.fromPage(page) #  this can be used for any page object
    #you can also define an item like this
    repo = site.data_repository()  # this is a DataSite object
    item = pywikibot.ItemPage(repo, 'Q42')  # This will be functionally the same as the other item we defined
    item.get() #  you need to call it to access any data.
    sitelinks = item.sitelinks
    aliases = item.aliases
    if 'en' in item.labels:
        print 'The label in English is: ' + item.labels['en']
    if item.claims:
        if 'P107' in item.claims:
            print item.claims['P107'][0].getTarget()
            print item.claims['P107'][0].sources[0] #  let's just assume it has sources.

    # Edit an existing item
    item.editLabels(labels={'language': 'en', 'value': 'Douglas Adams'}, summary=u'Edit label')
    item.editDescriptions(descriptions={'language': 'en', 'value': 'English writer'}, summary=u'Edit description')
    item.editAliases(aliases={'en':['An alias','Another alias']}, summary=u'Set aliases')
    item.setSitelink(sitelink={'site': 'enwiki', 'title': 'Douglas Adams'}, summary=u'Set sitelink')
    item.removeSitelink(site='enwiki', summary=u'Remove sitelink')

    #You can also made this all in one time:
    data = {'labels': {'language': 'en', 'value': 'Douglas Adams'},
      'descriptions': {'language': 'en', 'value': 'English writer'},
         'sitelinks': {'site': 'enwiki', 'title': 'Douglas Adams'}}
    item.editEntity(data, summary=u'Edit item')

CAUTION: The methods and results may be changed in the future

See also
--------

-  `Wikidata scripts <Manual:Pywikibot/Scripts#Wikidata>`__
-  `d:Wikidata:Creating a bot <d:Wikidata:Creating a bot>`__
-  `pywikidata <https://github.com/jcreus/pywikidata>`__

`Wikidata <Category:Pywikibot>`__
