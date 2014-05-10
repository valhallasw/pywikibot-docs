.. raw:: mediawiki

   {{MoveToMediaWiki}}

 Script which manages categories. This needs Python with at least v2.4
(not v2.3) as stated on `Using the python
wikipediabot <Using the python wikipediabot>`__.

Syntax
------

The syntax is:

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

python category.py [global-arguments] action [-option]

.. raw:: html

   </div>

where action can be one of these:

| ``* add         - mass-add a category to a list of pages``
| ``* remove      - remove category tag from all pages in a category``
| ``* move        - move all pages in a category to another category``
| ``* tidy        - tidy up a category by moving its articles into subcategories``
| ``* tree        - show a tree of subcategories of a given category``
| ``* listify     - make a list of all of the articles that are in a category``

and option can be one of these:

| ``* -person     - sort persons by their last name (for action 'add')``
| ``* -rebuild    - reset the database``
| ``* -from:      - The category to move from (for the move option)``
| ``                Also, the category to remove from in the remove option``
| ``                Also, the category to make a list of in the listify option``
| ``* -to:        - The category to move to (for the move option)``
| ``              - Also, the name of the list to make in the listify option``
| ``        NOTE: If the category names have spaces in them you may need to use``
| ``        a special syntax in your shell so that the names aren't treated as``
| ``        separate parameters.  For instance, in BASH, use single quotes,``
| ``        e.g. -from:'Polar bears'``
| ``* -batch      - Don't prompt to delete emptied categories (do it``
| ``                automatically).``
| ``* -summary:   - Pick a custom edit summary for the bot.``
| ``* -inplace    - Use this flag to change categories in place rather than``
| ``                rearranging them.``
| ``* -nodelsum   - An option for remove, this specifies not to use the custom``
| ``                edit summary as the deletion reason.  Instead, it uses the``
| ``                default deletion reason for the language, which is "Category``
| ``                was disbanded" in English.``
| ``* -overwrite  - An option for listify, this overwrites the current page with``
| ``                the list even if something is already there.``
| ``* -showimages - An option for listify, this displays images rather than``
| ``                linking them in the list.``
| ``* -talkpages  - An option for listify, this outputs the links to talk pages``
| ``                of the pages to be listified in addition to the pages``
| ``                themselves.``
| ``* -recurse    - Recurse through all subcategories of categories.``
| ``* -match      - Only work on pages whose titles match the given regex (for``
| ``                move and remove actions).``
| ``* -create     - An option for add: if a page doesn't exist, do not skip it,``
| ``                create it instead``

If action is "add", the following options are supported:

| ``-cat             Work on all pages which are in a specific category.``
| ``                 Argument can also be given as "-cat:categoryname" or``
| ``                 as "-cat:categoryname|fromtitle".``
| ``-catr            Like -cat, but also recursively includes pages in``
| ``                 subcategories, sub-subcategories etc. of the``
| ``                 given category.``
| ``                 Argument can also be given as "-catr:categoryname" or``
| ``                 as "-catr:categoryname|fromtitle".``
| ``-subcats         Work on all subcategories of a specific category.``
| ``                 Argument can also be given as "-subcats:categoryname" or``
| ``                 as "-subcats:categoryname|fromtitle".``
| ``-subcatsr        Like -subcats, but also includes sub-subcategories etc. of``
| ``                 the given category.``
| ``                 Argument can also be given as "-subcatsr:categoryname" or``
| ``                 as "-subcatsr:categoryname|fromtitle".``
| ``-uncat           Work on all pages which are not categorised.``
| ``-uncatcat        Work on all categories which are not categorised.``
| ``-uncatfiles      Work on all files which are not categorised.``
| ``-file            Read a list of pages to treat from the named text file.``
| ``                 Page titles in the file must be enclosed with ``\ ```brackets`` <brackets>`__
| ``                 or separated by newlines. Argument can also be given as``
| ``                 "-file:filename".``
| ``-filelinks       Work on all pages that use a certain image/media file.``
| ``                 Argument can also be given as "-filelinks:filename".``
| ``-yahoo           Work on all pages that are found in a Yahoo search.``
| ``                 Depends on python module pYsearch.  See yahoo_appid in``
| ``                 config.py for instructions.``
| ``-search          Work on all pages that are found in a MediaWiki search``
| ``                 across all namespaces.``
| ``-google          Work on all pages that are found in a Google search.``
| ``                 You need a Google Web API license key. Note that Google``
| ``                 doesn't give out license keys anymore. See google_key in``
| ``                 config.py for instructions.``
| ``                 Argument can also be given as "-google:searchstring".``
| ``-namespace       Filters the page generator to only yield pages in the``
| ``                 specified namespaces.  Separate multiple namespace``
| ``                 numbers with commas.``
| ``-interwiki       Work on the given page and all equivalent pages in other``
| ``                 languages. This can, for example, be used to fight``
| ``                 multi-site spamming.``
| ``                 Attention: this will cause the bot to modify``
| ``                 pages on several wiki sites, this is not well tested,``
| ``                 so check your edits!``
| ``-links           Work on all pages that are linked from a certain page.``
| ``                 Argument can also be given as "-links:linkingpagetitle".``
| ``-new             Work on the 60 newest pages. If given as -new:x, will work``
| ``                 on the x newest pages.``
| ``-imagelinks      Work on all images that are linked from a certain page.``
| ``                 Argument can also be given as "-imagelinks:linkingpagetitle".``
| ``-newimages       Work on the 100 newest images. If given as -newimages:x,``
| ``                 will work on the x newest images.``
| ``-ref             Work on all pages that link to a certain page.``
| ``                 Argument can also be given as "-ref:referredpagetitle".``
| ``-start           Specifies that the robot should go alphabetically through``
| ``                 all pages on the home wiki, starting at the named page.``
| ``                 Argument can also be given as "-start:pagetitle".``
| ``                 You can also include a namespace. For example,``
| ``                 "-start:Template:!" will make the bot work on all pages``
| ``                 in the template namespace.``
| ``-prefixindex     Work on pages commencing with a common prefix.``
| ``-titleregex      Work on titles that match the given regular expression.``
| ``-transcludes     Work on all pages that use a certain template.``
| ``                 Argument can also be given as "-transcludes:Template:Title".``
| ``-unusedfiles     Work on all description pages of images/media files that are``
| ``                 not used anywhere.``
| ``                 Argument can be given as "-unusedfiles:n" where``
| ``                 n is the maximum number of articles to work on.``
| ``-unwatched       Work on all articles that are not watched by anyone.``
| ``                 Argument can be given as "-unwatched:n" where``
| ``                 n is the maximum number of articles to work on.``
| ``-usercontribs    Work on all articles that were edited by a certain user :``
| ``                 Example : -usercontribs:DumZiBoT``
| ``-weblink         Work on all articles that contain an external link to``
| ``                 a given URL; may be given as "-weblink:url"``
| ``-withoutinterwiki Work on all pages that don't have interlanguage links.``
| ``                 Argument can be given as "-withoutinterwiki:n" where``
| ``                 n is some number (??).``
| ``-random          Work on random pages returned by ``\ ```Special:Random`` <Special:Random>`__\ ``.``
| ``                 Can also be given as "-random:n" where n is the number``
| ``                 of pages to be returned, else 10 pages are returned.``
| ``-randomredirect  Work on random redirect target pages returned by``
| ``                 ``\ ```Special:Randomredirect`` <Special:Randomredirect>`__\ ``.  Can also be given as``
| ``                 "-randomredirect:n" where n is the number of pages to be``
| ``                 returned, else 10 pages are returned.``
| ``-gorandom        Specifies that the robot should starting at the random pages ``
| ``                 returned by ``\ ```Special:Random`` <Special:Random>`__\ ``.``
| ``-recentchanges   Work on new and edited pages returned by ``\ ```Special:Recentchanges`` <Special:Recentchanges>`__\ ``.``
| ``                 Can also be given as "-recentchanges:n" where n is the number``
| ``                 of pages to be returned, else 100 pages are returned.``
| ``-redirectonly    Work on redirect pages only, not their target pages.``
| ``                 The robot goes alphabetically through all redirect pages``
| ``                 on the wiki, starting at the named page. The``
| ``                 argument can also be given as "-redirectonly:pagetitle".``
| ``                 You can also include a namespace. For example,``
| ``                 "-redirectonly:Template:!" will make the bot work on``
| ``                 all redirect pages in the template namespace.``

For the actions tidy and tree, the bot will store the category structure
locally in category.dump. This saves time and server load, but if it
uses these data later, they may be outdated; use the -rebuild parameter
in this case.

Or to do it all from the command-line,

Example
-------

Adding category
~~~~~~~~~~~~~~~

If your list of pages is in a file, enter:

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

python category.py add -file:FILENAME

.. raw:: html

   </div>

If you don't enter a filename, you will be prompted for a page that has
the file list.

Follow the on-screen instructions - you will be prompted for the
category name.

To create a new category from a list of persons, you will usually want
them to be sorted alphabetically by last name (assuming Western surname
conventions). E.g. Adding the "Artist" category to the page "Jane
Smith", it would be added in the form [[Category:Artists\|Smith, Jane]].
Type:

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

python category.py add -person

.. raw:: html

   </div>

and follow the on-screen instructions.

Move category
~~~~~~~~~~~~~

If you want to move all pages in a category to another category, you
could do the following:

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

python category.py move

.. raw:: html

   </div>

You will be prompted for the old category (that you also want to keep
but enter it)

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

OldCategoryname

.. raw:: html

   </div>

Enter the name of the category without the 'Category:' prefix.

You will now be prompted for the new category, now enter the old and new
Category like this:

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

NewCategoryName

.. raw:: html

   </div>

To do it all from the command-line, use the following syntax:

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

python category.py move -from:"OldCategoryname" -to:"NewCategoryName"

.. raw:: html

   </div>

For example, this syntax will move all pages in the category US to the
category United States.

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

python category.py move -from:US -to:'United States'

.. raw:: html

   </div>

.. raw:: mediawiki

   {{Manual:Pywikipediabot/Global_Options}}

See also
--------

-  w:fr:Aide:Pywikipedia/category.py

`category.py <Category:Pywikibot scripts>`__
