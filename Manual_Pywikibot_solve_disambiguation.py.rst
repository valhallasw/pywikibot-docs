.. raw:: mediawiki

   {{svn/pywikipedia}}

.. figure:: Solve disambiguation.py screenshot ck.jpg
   :alt: Helping you choose the right page out of several disambiguated ones.

   Helping you choose the right page out of several disambiguated ones.
**solve\_disambiguation.py** is a `python
bot <meta:Using the python wikipediabot>`__ script to help a human solve
links to `disambiguation <meta:disambiguation>`__ pages by presenting a
set of options.

Type in the disambiguation page on the command line. The program will
pick up the page, and create a menu of all outbound links found on the
page, with a unique number adjacent to each link. It will then
automatically loop over all pages which refer to the disambiguation
page, and show 30 characters of context on each side of the reference to
help you make the decision between the alternatives. It will ask you to
type the number of the appropriate replacement, and perform the change.

It is possible to choose to replace only the link (just type the number)
or replace both link and link-text (type '``r``\ ' followed by the
number).

Multiple references in one page will be scanned in order, but typing
'``n``\ ' (next) on any one of them will leave the complete page
unchanged. To leave only some reference unchanged, use the '``s``\ '
(skip) option.

Command line options (in addition to the general options for all bots):

-pos:XXXX
    adds ``XXXX`` as an alternative disambiguation
-just
    Only use the alternatives given on the command line, do not read the
    page for other possibilities.
-primary
    "Primary topic" disambiguation (Begriffsklärung nach Modell 2).
    That's titles where one topic is much more important, the
    disambiguation page is saved somewhere else, and the important topic
    gets the nice name. All links found on page
    ``XXXX&nbsp;(disambiguation)`` will be listed as options for the
    user, but the bot will still work on links to ``XXXX``.
-primary:XY
    Like the above, but use XY as the only alternative, instead of
    searching for alternatives in [[Keyword (disambiguation)]]. Note:
    this is the same as ``-primary -just -pos:XY``.
-file:XYZ
    Reads a list of pages, which can for example be gotten through
    extract\_names.py. XYZ is the name of the file from which the list
    is taken. If XYZ is not given, the user is asked for a filename.
    Page titles should be listed one per line, with [[brackets]].
    The ``-pos`` parameter won't work if ``-file`` is used.
-always:XY
    Instead of asking the user what to do, always perform the same
    action. For example, ``XY`` can be "r0", "u" or "2". **Be careful**
    with this option, and check the changes made by the bot. Note that
    some choices for XY don't make sense and will result in a loop,
    *e.g.*, "l" or "m".
-main
    Only check pages in the main namespace, not in the talk, wikipedia,
    user, etc. namespaces.
-first
    Uses only the first link of every line on the disambiguation page
    that begins with an asterisk. Useful if the page is full of
    irrelevant links that are not subject to disambiguation. You won't
    get all af them as options, just the first on each line. For a
    moderated example see `:en:Szerdahely <:en:Szerdahely>`__, and for a
    really exotic one `:hu:Brabant (egyértelműsítő
    lap) <:hu:Brabant (egyértelműsítő lap)>`__
-start:XY
    Goes through all disambiguation pages in the category on your wiki
    that is defined (to the bot) as the category containing
    disambiguation pages, starting at XY. If only '-start' or '-start:'
    is given, it starts at the beginning.

To complete a move of a page, one can use:

``   python solve_disambiguation.py -just -pos:New_Name Old_Name``

See also
--------

#. Manual:Pywikipediabot/user-config.py#Configuration (about sorting
   links)

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/solve disambiguation.py}}

`solve disambiguation.py <Category:Pywikibot scripts>`__
