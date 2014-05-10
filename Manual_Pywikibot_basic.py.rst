 **basic.py** is a script of the `Pywikipedia
bot <Using the python wikipediabot>`__ framework. It is not a complete
bot; rather, it is a template from which simple bots can be made. You
can rename it to mybot.py, then edit it in whatever way you want.

Parameters
----------

The following parameters are supported:

-dry:If given, doesn't do any real changes, but only shows what would
have been changed.

All other parameters will be regarded as part of the title of a single
page, and the bot will only work on that single page.

Example
-------

``python basic.py -dry User:MyUserName``

    This tries to add 'Text ' in front of the page *User:MyUserName*.
    Since the -debug option is given, the page wouldn't be changed.

`basic.py <Category:Pywikibot scripts>`__
