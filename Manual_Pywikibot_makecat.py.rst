 **makecat.py** is a script which lets you easily add pages to a
category of your choosing, based upon an investigation of links in
existing articles. Its potential applications are diverse, but it would
be especially helpful on wikis that do not yet have well-established
category trees. Used properly, it could create a number of fully
populated categories much more quickly than by manual editing.

This script is a standard part of the pywikipediabot installation, and
should be available to all users who have installed pywikipediabot
properly. However, in most installations of the pywikipedia script
library, it produces syntax errors and immediately aborts. These errors
have been present in the script's released version since at least 4Q
2009. They are, however, `easily corrected <#Error_correction>`__.
Although it does not work "out of the box" as of January 2012, you can
get it up and running in less than one minute.

Concept
-------

The basic idea of the script is straightforward, though it relies on an
assumption that may not be appropriate for all wikis. It allows you to
use the links on a page to quickly populate a category of your choosing.
It presumes, therefore, that pages about a certain topic will have links
that you want to put into a *category* about the *same* topic.

For instance, imagine you have a page called `American
football <American football>`__ and you want to quickly populate
`:category:American football
teams <:category:American football teams>`__. The script will go through
the text of the page, stopping on everything included in link brackets.
It will then ask you whether you want to put that linked page into the
`:category:American football
teams <:category:American football teams>`__. Assuming that `American
football <American football>`__ will contain links to `Wahington
Redskins <Wahington Redskins>`__, `Pittsburgh
Steelers <Pittsburgh Steelers>`__ and other teams would be linked on a
page about `American football <American football>`__, makecat.py would
thus save you a lot of time over going to each one of those team pages
and adding a category manually..

Syntax
------

The script is invoked by ``python makecat.py`` Without any parameters,
this will prompt you for a page to start with, and you'll then go from
there, depending on which pages you admit to your category. Despite the
ease of this arrangement, you'll probably want to add some parameters.
If you give no parameters, it assumes you want to add the discovered
pages in whatever category you were working on the **last time** you
used the bot.

A more specific syntax is:
``python makcecat.py "category name" -argument``

Note that *category name* should just be the *category name*, with
namespace and brackets excluded. Technically, the enclosing quotation
marks aren't *necessary*, but they are *allowed*. The *argument*
requires a prepending hyphen and can be one of a number of things, as
seen in the script's standard help file:

::

    This bot takes as its argument (or, if no argument is given, asks for it), the
    name of a new or existing category. It will then try to find new articles for
    this category (pages linked to and from pages already in the category), asking
    the user which pages to include and which not.

    Arguments:
       -nodates  automatically skip all pages that are years or dates (years
                 only work AD, dates only for certain languages)
       -forward  only check pages linked from pages already in the category,
                 not pages linking to them. Is less precise but quite a bit
                 faster.
       -exist    only ask about pages that do actually exist; drop any
                 titles of non-existing pages silently. If -forward is chosen,
                 -exist is automatically implied.
       -keepparent  do not remove parent categories of the category to be
                 worked on.
       -all      work on all pages (default: only main namespace)

    When running the bot, you will get one by one a number by pages. You can
    choose:
    Y(es) - include the page
    N(o) - do not include the page or
    I(gnore) - do not include the page, but if you meet it again, ask again.
    X - add the page, but do not check links to and from it
    Other possiblities:
    A(dd) - add another page, which may have been one that was included before
    C(heck) - check links to and from the page, but do not add the page itself
    R(emove) - remove a page that is already in the list
    L(ist) - show current list of pages to include or to check

So, to follow with our American football example,
``python makecat.py "American football teams" -keepparent -forward``
will do the following:

#. Assume that the page to start on is itself titled "American football
   teams", but give you the opportunity to choose a different starting
   page
#. Make sure that the category tree is undisturbed by keeping the parent
   of `:category:American football
   teams <:category:American football teams>`__, perhaps
   `:category:Sporting teams <:category:Sporting teams>`__, in place.
   (You should give strong consideration to almost always using the
   ``-keepparent`` argument.)
#. It will only search for pages which **exist** and are **linked to**
   on your page — in other words, pages that are actually *forward* of
   the one on which you're working

As the bot works and you accept certain pages into your new category, it
will then branch off and look from the pages that you add to the
category. So, imagine you find a link to `Dallas
Cowboys <Dallas Cowboys>`__ on `American
football <American football>`__. You accept that as a page that needs to
be in `:category:American football
teams <:category:American football teams>`__. The script will now also
scan `Dallas Cowboys <Dallas Cowboys>`__ for links. It's this additive
process that means you'll more quickly amass pages in your desired
category.

Not automated
-------------

There are no circumstances in which a reasonable wiki administrator
would ever want to automate this script, so no option for doing so is
included. Think of this as a "semi-automatic" script. It's still much
faster than just adding individual pages to a category, but it doesn't
work without human control of the bot.

Error correction
----------------

The version which is part of the standard pywikipedia script library as
of January 2012 is 7336, dated 2009-09-29. This code has a small syntax
error that needs to be corrected before the script can be used.

#. **Navigate** to makecat.py within your library. (On Macs, this is
   typically at
   ``''whatever_your_user_name_is''/pywikipedia/makecat.py``)
#. **Open** makecat.py by double-clicking on it. Unless you have a
   *very* barebones setup, your computer should automatically find a
   program capable of editing it. (On Macs, IDLE should instantly start
   on double click.)
#. **Navigate** down to the area just below the explanatory text at the
   top of the file. You'll see a raft of different translations of a
   one-line message. In English, this message says "creation or update
   of category". (If you're lost, just use your editor's search function
   to look for that phrase.)
#. **If you know a bit about javascript coding**, you'll be able to
   instantly see some glaring syntax errors at the end of the 'nn' and
   'no' lines. ``'nn':u'oppretting eller oppdatering av kategori:':``
   and ``'no':u'opprettelse eller oppdatering av kategori:':`` are the
   source of the problem.
#. **Change** the final colons to commas. The lines should read:
   ``'nn':u'oppretting eller oppdatering av kategori:',`` and
   ``'no':u'opprettelse eller oppdatering av kategori:',``
#. **Save** your file (Ctrl-S; or, if Mac, Command-S)

makecat.py will now work properly..
`makecat.py <category:Pywikibot scripts>`__
