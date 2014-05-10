.. raw:: mediawiki

   {{svn/pywikipedia}}

.. raw:: mediawiki

   {{Pywikibot|script}}

This Pywikibot bot script replaces a template with another, and converts
the old MediaWiki boilerplate format to the new template format.

Usage
-----

    Syntax:
    ``python template.py [-remove] [xml[:filename]] "oldTemplate" ["newTemplate"]``
    Example:
    ``python template.py "Cities in Washington" "Cities in Washington State"``

Specify the template on the command line. The program will pick up the
template page, and look for all pages using it. It will then
automatically loop over them, and replace the template.

Command line options
~~~~~~~~~~~~~~~~~~~~

+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -remove:       | Remove every occurence of the template from every article                                                                                                                                                                                                                               |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -subst:        | Resolves the template by putting its text directly into the article. This is done by changing {{...}} or {{msg:...}} into {{subst:...}}                                                                                                                                                 |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -assubst:      | Replaces the first argument as old template with the second argument as new template but substitutes it like -subst does. Using both options -remove and -subst in the same command line has the same effect.                                                                           |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -xml:          | retrieve information from a local dump (http://download.wikimedia.org). if this argument isn't given, info will be loaded from the maintenance page of the live wiki. argument can also be given as "-xml:filename.xml".                                                                |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -namespace:    | Only process templates in the given namespace number (may be used multiple times).                                                                                                                                                                                                      |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -summary:      | Lets you pick a custom edit summary. Use quotes if edit summary contains spaces.                                                                                                                                                                                                        |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -always:       | Don't bother asking to confirm any of the changes, Just Do It.                                                                                                                                                                                                                          |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -category:     | Appends the given category to every page that is edited. This is useful when a category is being broken out from a template parameter or when templates are being upmerged but more information must be preserved.                                                                      |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -user:         | Only edit pages for an user.                                                                                                                                                                                                                                                            |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| oldTemplate:   | old template name                                                                                                                                                                                                                                                                       |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| newTemplate:   | new template name. If only one argument is given, the bot resolves the template by putting its text directly into the article. This is done by changing {{...}} or {{msg:...}} into {{subst:...}}. If you want to address a template which has spaces, put quotation marks around it.   |
+----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Output
------

Example of output when running this bot (using windows which does not
need "python" typed in):

::

    C:\Users\t\Desktop\pywikipedia> template.py "TOCright" "TOCright test"
    Getting references to <nowiki>[[Template:TOCright]]</nowiki> via API...
    Getting 3 pages from dead:en...
    >>> '''<font color="purple">Talk:Zombrex Posters</font>''' <<<
    - <nowiki>{{TOCright}}</nowiki>
    + {{TOCright '''<font color="green">test</font>'''}}

    Do you want to accept these changes? ([y]es, [N]o, [e]dit, open in [b]rowser, [a]ll, [q]uit) n

    0 pages were changed.

`template.py <Category:Pywikibot scripts>`__
