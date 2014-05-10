.. raw:: mediawiki

   {{Pywikipediabot}}

This page is a short working summary of `Manual:Pywikipediabot/Use on
third-party wikis <Manual:Pywikipediabot/Use on third-party wikis>`__.
See that page for more detail if anything is not clear and if your wiki
has more namespaces, languages or uses other setups not discussed here.
Most of this should work for a single wiki site in the English language.
If you have a wiki in one non-English language, you can change the
family file accordingly (it's easy).

Before you try to create a bot, take a look at the
`scripts <Manual:Pywikipediabot/Scripts>`__ available. The scripts are
flexible and can do a lot of tasks but if one is not available for your
specific task, you might have to make one yourself in
`Python <:w:en:Python (programming language)>`__.

Requirements for a bot
----------------------

To run a bot on your wiki, you will need shell access to your hosting
account. If you don't know whether you have shell access or not, ask
your hosting provider. You will need Python version > 2.5 and less than
3.0, although Python 2.4.3 has also worked for at least one bot script.
The preferred version is 2.7.2. To check whether you have Python
installed and its version, just type "``python``\ " at the shell prompt.

.. raw:: mediawiki

   {{Manual:Pywikibot/Version table}}

For the compat version, every Python script (a ``.py`` file) is run by
entering the following on a Unix command prompt:

.. code:: bash

    python myscript.py

For the core version, the scripts should be run with ``pwb.py``, which
can be found in the root directory of pywikibot.

.. code:: bash

    python pwb.py myscript.py

Steps
-----

**What you'll be doing:** You will be creating a bot username on your
wiki, give rights to it, get the bot software, make two text files,
upload the software, log the bot in and run a test script to see if the
bot works.

1. Make a username for your bot, like someone would make a regular user
account on the wiki (e.g. SiteBot/password). Make sure to have a
reasonably secure password (not something easy like "sitebot123").

2. Logout from the bot account and login using a Bureaucrat account. In
the User rights, give that username "bot" rights. If you have the
Flagged revisions extension, give that bot "reviewer" and "editor"
rights.

3. **`Download <http://tools.wmflabs.org/pywikibot/>`__** The
Pywikipedia bot software on your computer. `Direct link to zip
file <http://toolserver.org/~pywikipedia/nightly/package/pywikipedia/pywikipedia-nightly.zip>`__
or see Downloads section for other formats.

4. Extract the contents of the zip file to a folder on your computer.
There will be many subfolders in that directory. All of this is the bot
software. Beware of non-English (accented) letters in the path, because
at least within Linux they caused problems in several cases. [1]_ [2]_

5. Inside the folder that you placed Pywikibot, create a text file with
the name "``user-config.py``\ " that has the following customized lines:

.. code:: python

     mylang='en'
     family = 'yoursite'
     usernames['yoursite']['en']=u'MySiteBot'
     console_encoding = 'utf-8'

Where you see "yoursite" for the family variable, use the name of your
site (``$wgSiteName``), all lower case letters.

For:

.. code:: python

    usernames['yoursite']['en']=u'SiteBot'

SiteBot is the name of your bot user account that you made in step 1.
Use correct case.

Save this file.

6. Upload the "``pywikipedia``\ " directory to your server. This
directory can be in the same location as your ``LocalSettings.php``
file.

7. Login to your shell account and navigate to that uploaded directory
on your server.

8. Now you'll create a family file for your site. First see if it can be
generated automatically. On the Shell prompt, type
"``python generate_family_file.py``\ " and press enter. If you get an
error and the file is not generated, then follow the example below.

For the **simplest** case where there's only one wiki in the English
language, here's an example from the Mozilla Wiki:

.. code:: python

    # -*- coding: utf-8  -*-
     
     import family
     
     # The official Mozilla Wiki. #Put a short project description here.
     
     class Family(family.Family):
     
         def __init__(self):
             family.Family.__init__(self)
             self.name = 'mozilla' # Set the family name; this should be the same as in the filename.
             self.langs = {
                 'en': 'wiki.mozilla.org', # Put the hostname here.
             }
     
             # Translation used on all wikis for the different namespaces.
             # Most namespaces are inherited from family.Family.
             # Check the family.py file (in main directory) to see the standard
             # namespace translations for each known language.
             # You only need to enter translations that differ from the default.
             self.namespaces[4] = {
                 '_default': u'MozillaWiki', # Specify the project namespace here.
             }
     
             self.namespaces[5] = {
                 '_default': u'MozillaWiki talk', # Specify the talk page of the project namespace here. 
             }
     
         def version(self, code):
             return "1.4.2"  # The MediaWiki version used. Not very important in most cases.
     
         def scriptpath(self, code):
             return '' # The relative path of index.php, api.php : look at your wiki address. 
    # This line may need to be changed to /wiki or /w, 
    # depending on the folder where your mediawiki program is located.
    # Note: Do not _include_ index.php, etc.

MyWiki/mywiki should be changed to reflect your wiki's name
(``$wgSiteName``)

This text file should be renamed "``mywiki_family.py``\ " (replace
mywiki with your wiki's name, all lowercase) and be uploaded to the
"``families``\ " folder (you'll find other family files there, they can
be ignored). You now have a family file for your site.

9. Now you'll login to your bot and see if it works. On the shell
prompt, in the "``pywikipedia``\ " directory, type in:
"``python pwb.py login.py``\ ". It should prompt for the bot's password
which you made in step 1. If it logs in, you'll see a 'success' message.
You only have to do this once. Bots usually stay logged in.

10. To test if your bot works or not, you can use an existing script
that adds text to the top of all pages in a certain category. On your
site, find a category that has only a few pages in it, not more than 10,
so you can revert them easily. If you don't have such a category, add a
temporary category to any 3 pages on the site.

At your shell command prompt, inside the pywikipedia directory again,
run the ``add_text`` script:

.. code:: bash

    python pwb.py add_text.py -cat:catname -text:"This is a Test." -except:"\{\{([Tt]emplate:|)[Dd]ocumentation [Ss]ubpage" -up

Replace catname in "``-cat:catname``\ ". The catname is the name of your
'test' category. For example if the title of the category page is
"Category:Test Pages", you will write "``-cat:test_pages``\ " in that
command.

This will insert the text "This is a Test." on top of all pages in that
test category.

If the bot is working, you'll see the shell command prompt change
according.

11. Go to your Recent Changes and click on "show bots" to see if your
bot made the edits.

For other bots, see: Manual:Pywikipediabot/Scripts and
`Manual:Pywikipediabot/Create your own
script <Manual:Pywikipediabot/Create your own script>`__. If you can't
find a bot that will do the stuff you want it to do, you can see the
existing scripts for suggestions on how you could make your own bot.

When you run a new untested bot script, run it on a "test" wiki in case
it goes out of control. You can also block it like you would block a
regular wiki username. You can also quit the shell prompt.

Notes
-----

.. raw:: html

   <references />

`Quick Start Guide <Category:Pywikibot>`__

.. [1]
   `SourceForge bug
   report <https://sourceforge.net/tracker/?func=detail&aid=3428890&group_id=93107&atid=603138>`__

.. [2]
   `Bug report in Hungarian
   Wikipedia <http://hu.wikipedia.org/w/index.php?title=Wikip%C3%A9dia:Botgazd%C3%A1k_%C3%BCzen%C5%91fala&diff=11207548&oldid=11207531#Pywikipedia_hiba.C3.BCzenet>`__
   (in Hungarian)
