Tips for core branch
~~~~~~~~~~~~~~~~~~~~

Here and in `wikipedia.py <Manual:Pywikipediabot/Wikipedia.py>`__, there
are some very basic tips for getting started writing your own bot. Make
sure you've set up your user-config.py file!

You can either use the following commands in a shell, or in a script.

To open a shell, run ``python pwb.py shell``;

As a script, please save the file as 'myscript.py' in the 'scripts/'
directory; then run ``python pwb.py myscript``.

-  To gain access to the pywikipedia framework, use:

.. code:: python

    import pywikibot

-  to retrieve a page, use the following, where pageName is, e.g.,
   "Wikipedia:Bots" or "India":

.. code:: python

    site = pywikibot.Site()
    page = pywikibot.Page(site, u"pageName")
    text = page.text

-  to update a page, use:

.. code:: python

    page.text = u"newText"
    page.save(u"Edit comment")

-  look at some of the pywikibot files for other ideas --
   scripts/basic.py is relatively easy to read even if you're new to
   pywikibot.
-  you can find all available Page methods in the pywikibot/page.py
   file.
-  basic.py gives you a setup that can be used for many different bots,
   all you have to do is define the string editing on the page text.
-  To `iterate <:w:iteration>`__ over a set of pages, see
   pywikibot/pagegenerators.py for some objects that return a set of
   pages. An example use of the CategoryPageGenerator that does
   something for each page in the `Category:Living
   people <:w:Category:Living people>`__ category:

.. code:: python

    import pywikibot
    from pywikibot import pagegenerators
    site = pywikibot.Site()
    cat = pywikibot.Category(site,'Category:Living people')
    gen = pagegenerators.CategorizedPageGenerator(cat)
    for page in gen:
      #Do something with the page object, for example:
      text = page.text

