.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/login.py}}

.. raw:: mediawiki

   {{svn/pywikipedia}}

.. raw:: mediawiki

   {{Pywikibot|script}}

**login.py** is the python program that logs the user running the
pywikipedia bot on to the system using the data that can be found in
**`user-config.py <Pywikipediabot/user-config.py>`__**.

Logging in as a bot
-------------------

Bots provide specified result and as a consequence, they should not need
the attention that other changes require. By having a specific user to
run the bot software, the changes created in this way will be hidden on
a typical **recent changes** screen. Bot status is given when a
community is in favour with someone running a bot.

If you want to login also with your sysop account (deleting moved
categories...) you have to add

::

    sysopnames['wikiproject']['languagecode'] = u'YourSysopUsername'

to *user-config.py* and start *login.py* with the **-sysop** parameter

How it knows where to login
---------------------------

In the user-config.py file there are three components:

#. the language: mylang
#. the family: family - this indicates wiki name, including
   `wikipedia <wikipedia>`__ or `wiktionary <wiktionary>`__
#. the username: username - this can be any user but it should be a user
   who is registered to run as a bot.

In order to login to all the projects/languages mentioned in
user-config.py, the option ``-all`` can be used, and if the same
password is used throughout all these projects, it can be combined with
``-pass`` so that the program doesn't ask for a password for each site.

``login.py -all -pass``

will login on all projects in user-config.py, using the same password
for all.

.. raw:: mediawiki

   {{:Manual:Pywikipediabot/Global_Options}}

See also
--------

-  `Using the python wikipediabot <Using the python wikipediabot>`__

`login.py <Category:Pywikibot scripts>`__
