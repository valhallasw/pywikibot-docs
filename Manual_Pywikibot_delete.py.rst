.. raw:: mediawiki

   {{MoveToMediaWiki}}

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/delete.py}}

 This script can be used to delete pages en masse. You will need an
admin account on the relevant wiki. Also add:

``sysopnames['wikipedia']['en'] = 'adminname'``

To ``user-config.py``

Where ``['wikipedia']`` is the name of the the family in which you are
working on, and ``'adminname'`` is the username.

Examples
~~~~~~~~

-  Delete everything in the category "To delete" without prompting.

``python delete.py -cat:"To delete" -always``

-  Delete everything in the pages linked to the page, without prompting.

``python delete.py "deletepage" -always``

-  Delete pages inside a text file:

``python delete.py -file:nuke.txt -always -summary:"Because I feel like it"``

The format of the text file should be as the following:

::

    <nowiki>
    # [[Main Page]]
    # [[Talk:Main Page]]
    </nowiki>

-  Restore pages:

``python delete.py -undelete -file:respawn.txt -summary:"It was a foolish mistake"``

Arguments
~~~~~~~~~

-  -cat: Delete all pages in the given category.
-  -links: Delete all pages linked from a given page.
-  -always Don't prompt to delete pages, just do it.
-  -summary: Supply a custom edit summary.
-  -undelete: Actually undelete pages instead of deleting. Works only
   with -page and -file.
-  -file: Delete all pages listed in a given text file. The list should
   be of the format

   -  ``<nowiki># [[page1]] </nowiki>``
   -  ``<nowiki># [[page2]]</nowiki>``
   -  ``''etc.''``

Usage output
~~~~~~~~~~~~

Usage is reported thus;

| ``Global arguments available for all bots:``
| ``-lang:xx          Set the language of the wiki you want to work on, overriding``
| ``                  the configuration in user-config.py. xx should be the``
| ``                  language code.``
| ``-family:xyz       Set the family of the wiki you want to work on, e.g.``
| ``                  wikipedia, wiktionary, wikitravel, ...``
| ``                  This will override the configuration in user-config.py.``
| ``-log              Enable the logfile. Logs will be stored in the logs``
| ``                  subdirectory.``
| ``-log:xyz          Enable the logfile, using xyz as the filename.``
| ``-nolog            Disable the logfile (if it is enabled by default).``
| ``-putthrottle:nn   Set the minimum time (in seconds) the bot will wait between``
| ``                  saving pages.``
| ``This script can be used to delete and undelete pages en masse.``
| ``Of course, you will need an admin account on the relevant wiki.``
| ``Syntax: python delete.py [-cat:categoryName|-page:pageName|...] [-summary:"text"] [-undelete] [-always]``
| ``Command line options:``
| ``-page:       Delete specified page``
| ``-cat:        Delete all pages in the given category.``
| ``-links:      Delete all pages linked from a given page.``
| ``-file:       Delete all pages listed in a text file.``
| ``-ref:        Delete all pages referring from a given page.``
| ``-images:     Delete all images used on a given page.``
| ``-always:     Don't prompt to delete pages, just do it.``
| ``-summary:    Supply a custom edit summary.``
| ``-undelete:   Actually undelete pages instead of deleting.``
| ``             Obviously makes sense only with -page and -file.``

Examples:

Delete everything in the category "To delete" without prompting.

| ``    python delete.py -cat:"To delete" -always``

`delete.py <Category:Pywikibot scripts>`__
