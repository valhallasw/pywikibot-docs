Pywikipediabot 2.0 aka "rewrite" was proposed in
`2007 <botwiki:Rewrite>`__, but has never been ready to replace the
current "trunk" version. This is a list of things that we should do to
get it ready.

Goals
-----

-  Be ready to merge at the end of Summer 2013.
-  Provide a seamless transition for bot operators and writers.
-  Make it easier to make raw API calls.
-  Proper distinction between programs (give output and user
   interaction) and libraries

To be done
----------

-  Many site methods not yet implemented.
-  All trunk scripts should be converted over. (`/Porting
   status </Porting status>`__)
-  Create a script called ``wikipedia.py`` to provide a compatibility
   layer. (`/Conversion </Conversion>`__)
-  Some programs need to be split into a program and library part (for
   example upload.py)
-  login.py has some weird quirks that need to be looked into (hack
   workaround at `/login.py </login.py>`__, maybe this has to do with
   the path itself?)
-  Move api.update\_page to a method of the page class
-  Find a way to cache tokens between login sessions.
-  Unit tests

   -  All the unit tests for ``i18n.twtranslate`` are failing.

-  Documentation, documentation, documentation!

Ideas
-----

-  Python3 compatibility!

   -  As a general tip, all code committed now should try to be as
      Python3 compatible as possible. (Don't use {}.has\_key, use 'key'
      in {}, etc)

-  Replace Page.templatesWithParams with a true parser,
   `mwparserfromhell <https://github.com/earwig/mwparserfromhell>`__, by
   `User:The Earwig <User:The Earwig>`__ and `User:Σ <User:Σ>`__
-  Content+Site model is needed. The current structure of pywiki centers
   around a "page" object. This object is both the container of data,
   plus the networking code. It allows someone to write page.content()
   to get the page markup from a site, which might be somewhat
   convenient, yet it promotes non-batched usage which is much heavier
   on wiki. Instead, page object should be a local-only container of
   data and related (parsing) code, whereas all network access should be
   done by the Site object. Syntax might be different, but the concepts
   should stay:

.. code:: python

    page1 = Page('Main Page')
    batch = [page1,page2,page3]
    site.populateStuff(batch, content | links | categories) # Sets various properties in the batch based on bit flags
    batch2 = site.query({api parameters}) # page objects are created from a result of a user-supplied query
    print(page1.links()) # list of links.
    print(page1.templates()) # throws an error - templates are not populated

--`Yurik <User:Yurik>`__ (`talk <User talk:Yurik>`__) 06:13, 22 March
2013 (UTC)

See also
--------

-  `/Conversion </Conversion>`__
-  `/Porting status </Porting status>`__

`#2.0 <Category:Pywikibot>`__
