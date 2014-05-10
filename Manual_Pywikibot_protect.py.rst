 **protect.py** is a script that helps you `protect
pages <help:protected pages>`__ *en masse*. It is a simple script that
gives you great power over the protected status of `almost
every <#Limitations>`__ part of your wiki. However, since wikis are
generally thought of as "encyclopedias *anyone* can edit", some thought
must be giving to the reasons why you want to use this script. Within
some wiki communities, particularly Wikipedia itself, misuse of this
script could well result in the revocation of your sysop rights.

When to use
-----------

Before using this script, you need to thoroughly understand your wiki's
policies about page protection. If your wiki hasn't yet discussed its
page protection philosophy, it's a good idea to have that discussion and
to write up some kind of policy **before using this script**. Your
community should understand what you're doing with the bot. Misuse of
this bot — that is, using it to protect *all* pages on a wiki — is
*very* easy to do with this bot, but would generally be seen as an abuse
of administrative powers in most wiki communities. Remember: you could
prevent all non-admin from editing **every page on your wiki** by
issuing **just one command** with this script.

Typical *reasonable* usages are:

-  protecting a whole category of templates, because changing those
   templates would have a significant impact upon the wiki
-  protecting help or policy pages from general editing, because you
   don't want the "rules" of your wiki being subject to vandalism
-  preventing pages from having their names changed — that is, "move
   locking" pages — but still allowing them to be freely edited

Syntax
------

The script is invoked by typing:

    ``python protect.py ''parameter1'' ''parameter2'' . . . ''parameterX'' ``

Available parameters include:

::

    -page:       Protect specified page
    -cat:        Protect all pages in the given category.
    -nosubcats:  Don't protect pages in the subcategories.
    -links:      Protect all pages linked from a given page.
    -file:       Protect all pages listed in a text file.
    -ref:        Protect all pages referring from a given page.
    -images:     Protect all images used on a given page.
    -always:     Don't prompt to protect pages, just do it.
    -summary:    Supply a custom edit summary.
    -unprotect:   Actually unprotect pages instead of protecting
    -edit:PROTECTION_LEVEL Set edit protection level to PROTECTION_LEVEL
    -move:PROTECTION_LEVEL Set move protection level to PROTECTION_LEVEL

    ## Without support ##
    ## -create:PROTECTION_LEVEL Set move protection level to PROTECTION_LEVEL ##

    Values for PROTECTION_LEVEL are: sysop, autoconfirmed, none.
    If an operation parameter (edit, move or create) is not specified, default
    protection level is 'sysop' (or 'none' if -unprotect).

Usage
-----

Following are some concrete examples of typical usages.

Complete lockdown of everything in a category
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First, consider the case of a category called `:category:Dependent
templates <:category:Dependent templates>`__. Everything in this
category is a template which *requires* another template to work. On its
own, no template in this category does *anything*. But if the template
gets changed, it will have a knock-on effect for other templates, which
themselves might be transcluded on other pages. So we definitely want to
protect these templates from harm. They're the building blocks of our
wiki! Here's how you do it.

    ``python protect.py -cat:"Dependent templates" -summary:"Moving or editing this template will harm other templates."``

Easy. No options other than the category name and a summary. The script
will assume you want to move- and edit-lock the template, so you don't
need to do anything else.

Move-locking
~~~~~~~~~~~~

Now, imagine that you run a wiki about a television show. Your community
has decided on a standard nomenclature for the naming of pages about
episodes of that show. There will never be a foreseeable need to change
that nomenclature, and it would require a big community discussion to do
so, anyway. So you want to protect pages from being moved (renamed).
Here's how you do it:

    ``python protect.py -cat:Episodes -move:sysop -edit:none -summary:"This article's name has been agreed by consensus at [[Forum:Episode names]].  It should not be moved."``

Note a few things here.

-  We don't need to put the category name into quotation marks, because
   it's just one word. (This is, incidentally, true of almost every
   pywikipedia script.)
-  The summary must be in double quotations, because we've included an
   apostrophe in the summary text
-  The ``-edit`` parameter must be defined to ``none`` if we want to
   allow everyone to edit the article, because ``-edit, -move`` and
   ``-create`` all default to ``sysop``
-  Defining ``-create`` in this instance would have no effect, because
   the pages in a category are already created

Working from a text file
~~~~~~~~~~~~~~~~~~~~~~~~

Now for a more complicated case. Imagine you wanted to protect the *most
used* templates on your wiki. This is a perfectly reasonable usage,
since changing a template that has 10,000 transclusions is going to have
a significant impact on your wiki. You quite rightly don't want such a
change happening on a whim. So, first you'd go to
Special:MostLinkedTemplates and extract the list into a text file called
``articles_list.txt``. Making sure that ``articles_list.txt`` was saved
to the ``pywikipedia`` folder on your computer, you'd then be able to
type something like this:

    ``python protect.py -file:articles_list.txt -always -summary:"[[Special:MostLinkedTemplates]] protection" -edit:sysop -move:sysop``

Custom summaries advisable
--------------------------

If you fail to use the ``-summary`` parameter, an automated summary will
be inserted for you. But that summary won't tell your community *why*
you've taken the action. Because protecting pages is generally
considered antithetical to the spirt of wiki editing, it's usually
important to leave behind a summary that explains *why* you've taken
this unusual action. Remember, when your users attempt to edit or move
the page, they'll get a message which includes your bot's edit summary.
In most cases, this summary should be as explicit as possible about the
reason why your users can't do what they want to do.

If you've put up a full block — that is, sysop-only editing — you'll
probably also want to include a link to a page where users can leave
feedback on how to improve the locked article. Often, this is the talk
page, but on wikis that don't have the talk page functionality enabled,
it might be a good idea to drop in a link to a forum or other feedback
page.

Limitations
-----------

This script has no ability to affect the protection level of anything in
the MediaWiki or Special namespaces. MediaWiki pages are *always*
"sysop-only" pages.

`protect.py <Category:Pywikibot scripts>`__
