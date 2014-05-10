.. raw:: mediawiki

   {{MoveToMediaWiki}}

 **Imageharvest.py** is a script of the `Pywikipedia
Bot <Using the python wikipediabot>`__ framework. It is used to copy
multiple images to a wiki. It takes a URL as an argument and finds all
images (and other files specified by the extensions in 'fileformats')
that URL is referring to, asking whether to upload them. If further
arguments are given, they are considered to be the text that is common
to the descriptions.

A second use is to get a number of images that have URLs only differing
in numbers. To do this, use the command line option "-pattern", and give
the URL with the variable part replaced by '$' (if that character occurs
in the URL itself, you will have to change the bot code, my apologies).

Other options:

::

    -shown      Choose images shown on the page as well as linked from it
    -justshown  Choose _only_ images shown on the page, not those linked

Syntax:

::

        python imageharvest.py http://www.sitename.org/folder 

Questions asked
---------------

When the bot is run, the bot will ask four questions (the web address is
an example):

::

    What text should be added at the end of the description of each image from this url? 

    Include image http://images.wikia.com/dead/images/b/bc/wiki.png? ([y]es, [N]o, [s]top) 

    Give the description of this image: 

    Specify a category (or press enter to end adding categories)

.. raw:: mediawiki

   {{Manual:Pywikibot/Global_Options}}

`imageharvest.py <Category:Pywikibot scripts>`__
