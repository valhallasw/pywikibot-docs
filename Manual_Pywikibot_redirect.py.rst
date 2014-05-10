.. raw:: mediawiki

   {{MoveToMediaWiki}}

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/redirect.py}}

.. raw:: mediawiki

   {{svn/pywikipedia}}

.. raw:: mediawiki

   {{Pywikibot|script}}

Script which fixes double redirects, and deletes broken redirects.

Requires access to MediaWiki's maintenance pages or to a XML dump file.
Delete function requires adminship.

Syntax
------

Syntax:

`` python redirect.py ``\ *``action``*\ `` ``\ *``[-argument]``*

where *action* can be one of these:

-  double - fix redirects which point to other redirects
-  broken - delete redirects where targets don't exist. Requires
   adminship, otherwise it will paste `db-r1 <Template:db-r1>`__ to call
   a human admin.

and *argument* (optional) can be:

-  xml:filename.xml - Retrieve information from a local XML dump
   (http://download.wikimedia.org). If this argument isn't given, info
   will be loaded from a special page of the live wiki. Cannot be used
   with moves or api.
-  api - Retrieve information using Mediawiki's API. Cannot be used with
   xml.
-  moves - Instead of using Special:Doubleredirects, use the page move
   log to find double-redirect candidates (only works with action
   "double", does not work with -xml)
-  namespace:n - Namespace to process. Works only with an XML dump or
   API. Can be repeated multiple times.
-  offset:n - With XML number of redirect to restart with (see
   progress). With -moves, the number of hours ago to start scanning
   moved page
-  always - Don't prompt you for each replacement.
-  start:page - with API start page
-  until:page - with API last page
-  number:page - with API number of pages to process

If neither api nor api nor moves are present, information will be loaded
using a special page

Example
-------

This syntax fixes all the double redirects. Since no argument is
defined, it uses Special:DoubleRedirects of the live wiki to find double
redirects by default. It will ask for confirmation before making
changes:

`` redirect.py double``

.. raw:: mediawiki

   {{:Manual:Pywikibot/Global Options}}

`redirect.py <Category:Pywikibot scripts>`__
