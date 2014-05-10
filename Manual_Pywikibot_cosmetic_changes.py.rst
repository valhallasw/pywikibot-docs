.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/cosmetic changes.py}}

.. raw:: mediawiki

   {{MoveToMediaWiki}}

 **cosmetic\_changes.py** makes little changes in one or several wiki
pages that make the source code look cleaner. These changes are not
supposed to change the look of the rendered wiki pages.

Before running it on a specific wiki, each sub-module should be reviewed
and checked if it is helpful for this wiki.

This script performs the following operations: [1]_

-  *fix self interwiki*: interwiki links to the site itself are
   displayed like local links, removing their language code prefix.
-  *standardize page footer*: makes sure that categories, stars
   templates for featured articles and interwiki links are put to the
   correct position. templates and interwiki links are sorted into the
   right order.
-  *clean up links*: improves how links are presented by doing the
   following:

   -  replaces underlines by spaces, also multiple underlines.
   -  removes unnecessary leading spaces from a title.
   -  removes unnecessary trailing spaces from a title.
   -  converts URL-encoded characters to unicode.
   -  removes unnecessary initial and final spaces from a label.
   -  tries to capitalize the first letter of the title.

-  *clean up section headers*: for better readability of section header
   source code, puts a space between the equal signs and the title; for
   example: "==Section title==" becomes "== Section title ==" .
-  *put spaces in lists*: for better readability of bullet list and
   enumeration wiki source code, puts a space between the \* or # and
   the text.
-  *translate and capitalize namespaces*: makes sure that localized
   namespace names are used. Does not change "image" alias on en-wiki or
   fr-wiki.
-  *resolve html entities*
-  *valid xhtml*: tries to make a valid XHTML document, for example,
   replacing "<br>" with "<br />"
-  *remove useless spaces*
-  *remove non breaking space before percent*: newer MediaWiki versions
   automatically place a non-breaking space in front of a percent sign,
   so it is no longer required to place it manually.
-  *fix syntax*: correct mediawiki syntax for external links
-  *fix HTML*: translates some HTML-entities into the corresponding
   mediawiki syntax; remove unneeded <ref /> tag.
-  *fix style*: convert prettytable to wikitable class (de-wiki and
   en-wiki only).
-  *fix typo*: change ccm with preleading number to cm³; change º to °
   if it concerns degree Celsius or Fahrenheit
-  *hyphenate isbn numbers*: tries to hyphenate an ISBN

References
----------

.. raw:: html

   <references/>

See also
--------

-  `Using the python wikipediabot <Using the python wikipediabot>`__
-  `:Commons:Commons:Tools/pywiki file description
   cleanup <:Commons:Commons:Tools/pywiki file description cleanup>`__
   version for use at Commons

`cosmetic changes.py <Category:Pywikibot scripts>`__

.. [1]
   `source code, function
   "change" <http://svn.wikimedia.org/svnroot/pywikipedia/trunk/pywikipedia/cosmetic_changes.py>`__
