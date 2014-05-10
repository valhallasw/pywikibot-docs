.. raw:: mediawiki

   {{MoveToMediaWiki}}

 **standardize\_notes.py** is a `python
bot <Using the python wikipediabot>`__ script for improving references
and citations.

The current version

-  Uses en:Wikipedia:Footnotes numbered link format through "ref" and
   "note" templates.
-  Converts inline URLs to Footnotes format links to citation entries.
-  Converts older link formats such as Footnotes2 to Footnotes format.
-  Searches for existing footnotes or citations in several section
   names, such as "Notes" or "References".
-  Creates citation entries using en:WP:CITE citation templates.

   -  For citations for which only a URL is known, attempts to access
      the URL.

      -  Attempts to get title information from HTTP or PDF information.

   -  "Web reference" citations are created by default.
   -  "News reference" citations are created for certain URLs.

-  Rebuilds notes section in same sequence as text references.
-  Some multiple references are converted to "ref\_label" and
   "note\_label" multiple links.
-  Detects some duplicate citations, labels them with "see above".
-  Keeps existing notes, does not yet examine content of notes other
   than leading "\*" or "#" list indicator.

Default behavior includes displaying changes and asking for confirmation
to perform the intended changes.

If no title information is found or there are errors in accessing the
URL, the title will contain the URL.

Command line options (in addition to the general options for all bots):

-sql
    Retrieve information from a local SQL dump (cur table, see
    http://download.wikimedia.org).

    -  Argument can also be given as "-sql:filename".

-file
    Work on all pages given in a local text file.

    -  Will read any `wiki link <wiki link>`__ and use these articles.
    -  Argument can also be given as "-file:filename".

-cat
    Work on all pages which are in a specific category.

    -  Argument can also be given as "-cat:categoryname".

-page
    Only edit a single page.

    -  Argument can also be given as "-page:pagename". You can give this
       parameter multiple times to edit multiple pages.

-regex
    Make replacements using regular expressions. (Obsolete; always True)
-except:XYZ
    Ignore pages which contain XYZ. If the -regex argument is given, XYZ
    will be regarded as a regular expression.
-namespace:n
    Namespace to process. Works only with a sql dump.
-always
    Don't prompt you for each replacement.

To process a single page page, one can use:

``   python standardize_notes.py -page:Somepage``

`standardize notes.py <Category:Pywikibot scripts>`__
