 **pagegenerators.py** can generate a list of pages.

Parameters
----------

The following is based on the comments within the pagegenerators.py file
itself.

Example:

``python pagegenerators.py -search:'foobar'``

This will return, in standard output, a list of all pages containing
"foobar," as returned by MediaWiki's search engine.

This module offers a wide variety of page generators. A page generator
is an object that is iterable (see
http://www.python.org/dev/peps/pep-0255/ ) and that yields page objects
on which other scripts can then work.

In general, there is no need to run this script directly. It can,
however, be run for testing purposes. It will then print the page titles
to standard output.

These parameters are supported to specify which pages titles to print:

-cat:Work on all pages which are in a specific category. Argument can
also be given as "-cat:categoryname" or as
"-cat:categoryname\|fromtitle".

-catr: Like -cat, but also recursively includes pages in subcategories,
sub-subcategories etc. of the given category. Argument can also be given
as "-catr:categoryname" or as "-catr:categoryname\|fromtitle".

-subcats: Work on all subcategories of a specific category. Argument can
also be given as "-subcats:categoryname" or as
"-subcats:categoryname\|fromtitle".

-subcatsr: Like -subcats, but also includes sub-subcategories etc. of
the given category. Argument can also be given as
"-subcatsr:categoryname" or as "-subcatsr:categoryname\|fromtitle".

-uncat: Work on all pages which are not categorised.

-uncatcat: Work on all categories which are not categorised.

-uncatfiles: Work on all files which are not categorised.

-file: Read a list of pages to treat from the named text file. Page
titles in the file must be enclosed with `brackets <brackets>`__ or
separated by newlines. Argument can also be given as "-file:filename".

-filelinks: Work on all pages that use a certain image/media file.
Argument can also be given as "-filelinks:filename".

-yahoo: Work on all pages that are found in a Yahoo search. Depends on
python module pYsearch. See yahoo\_appid in config.py for instructions.

-search: Work on all pages that are found in a MediaWiki search across
all namespaces.

-google: Work on all pages that are found in a Google search. You need a
Google Web API license key. Note that Google doesn't give out license
keys anymore. See google\_key in config.py for instructions. Argument
can also be given as "-google:searchstring".

-namespace: Filters the page generator to only yield pages in the
specified namespaces. Separate multiple namespace numbers with commas.

-interwiki: Work on the given page and all equivalent pages in other
languages. This can, for example, be used to fight multi-site spamming.
Attention: this will cause the bot to modify pages on several wiki
sites, this is not well tested, so check your edits!

-links: Work on all pages that are linked from a certain page. Argument
can also be given as "-links:linkingpagetitle".

-new: Work on the 60 newest pages. If given as -new:x, will work on the
x newest pages.

-imagelinks: Work on all images that are linked from a certain page.
Argument can also be given as "-imagelinks:linkingpagetitle".

-newimages: Work on the 100 newest images. If given as -newimages:x,
will work on the x newest images.

-ref: Work on all pages that link to a certain page. Argument can also
be given as "-ref:referredpagetitle".

-start: Specifies that the robot should go alphabetically through all
pages on the home wiki, starting at the named page. Argument can also be
given as "-start:pagetitle". You can also include a namespace. For
example, "-start:Template:!" will make the bot work on all pages in the
template namespace.

-prefixindex: Work on pages commencing with a common prefix.

-titleregex: Work on titles that match the given regular expression.

-transcludes: Work on all pages that use a certain template. Argument
can also be given as "-transcludes:Title" (without Template:prefix).

-unusedfiles: Work on all description pages of images/media files that
are not used anywhere. Argument can be given as "-unusedfiles:n" where n
is the maximum number of articles to work on.

-unwatched: Work on all articles that are not watched by anyone.
Argument can be given as "-unwatched:n" where n is the maximum number of
articles to work on.

-usercontribs: Work on all articles that were edited by a certain user :
Example : -usercontribs:DumZiBoT

-weblink: Work on all articles that contain an external link to a given
URL; may be given as "-weblink:url"

-withoutinterwiki: Work on all pages that don't have interlanguage
links. Argument can be given as "-withoutinterwiki:n" where n is some
number (??).

-random: Work on random pages returned by Special:Random. Can also be
given as "-random:n" where n is the number of pages to be returned, else
10 pages are returned.

-randomredirect: Work on random redirect target pages returned by
Special:Randomredirect. Can also be given as "-randomredirect:n" where n
is the number of pages to be returned, else 10 pages are returned.

-gorandom: Specifies that the robot should starting at the random pages
returned by Special:Random.

-recentchanges: Work on new and edited pages returned by
Special:Recentchanges. Can also be given as "-recentchanges:n" where n
is the number of pages to be returned, else 100 pages are returned.

-redirectonly: Work on redirect pages only, not their target pages. The
robot goes alphabetically through all redirect pages on the wiki,
starting at the named page. The argument can also be given as
"-redirectonly:pagetitle". You can also include a namespace. For
example, "-redirectonly:Template:!" will make the bot work on all
redirect pages in the template namespace.

Calls from another program
--------------------------

Category crawler:

.. code:: python

    import pagegenerators

    cat = catlib.Category(site, u'Category:Example')
    pages = cat.articlesList(False)
    for Page in pagegenerators.PreloadingGenerator(pages,100):
        treatment(Page.title())

Subcategories explorer:

.. code:: python

    gen = pagegenerators.CategorizedPageGenerator(categoryPage, recurse=True)

MySQL requests:

.. code:: python

    gen = pagegenerators.MySQLPageGenerator(query)

Please see the file content for more info.

Unicode recommendation
~~~~~~~~~~~~~~~~~~~~~~

The following code returns KeyError: 'query' because of the special
character:

.. code:: python

    gen = pagegenerators.SearchPageGenerator(u'´', namespaces = "0")

Consequently, `an encoding
conversion <http://toolserver.org/~jackpotte/unicode-HTML.html>`__ is
needed:

.. code:: python

    gen = pagegenerators.SearchPageGenerator("&#180;", namespaces = "0")

`pagegenerators.py <Category:Pywikibot scripts>`__
