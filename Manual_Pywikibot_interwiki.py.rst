.. raw:: mediawiki

   {{MoveToMediaWiki}}

.. raw:: mediawiki

   {{Languages|Manual:Pywikipediabot/interwiki.py}}

 Interwiki.py creates Interlanguage links between the different language
versions of a project.

Getting started
---------------

To see what you need to get started on the Python Wikipedia bot, see
`Using the python wikipediabot <Using the python wikipediabot>`__. We
assume you have taken these steps (downloading Python and bot, creating
``user-config.py``, running ``login.py``). Now to start, type
"interwiki.py" (without the "s"), or if that does not work, "python
interwiki.py".

The bot will ask for a page to check. Give a page on your home
Wikipedia, preferably one with one or more interwiki-links that could
however have more. The bot will read this page, and if it has any
interwiki-links, it will check those pages as well, and the
interwiki-links from those, etcetera. After it has finished that, what
happens depends on what pages it found.

-  If the page has no interwiki links, or if the links found are
   identical to the ones on the page, the bot will stop silently.
-  If the bot finds interwiki links to new languages, or finds that an
   interwiki-link has to be changed, it will do so.
-  If the bot finds that an interwiki link is to be removed, it will ask
   your permission to do so.
-  If the bot finds more than one page for a language, it will go into
   an interactive mode. It will give the pages found with the pages that
   link to that page, and ask for each language with more than one link,
   which if any should be linked to, then ask for each language with one
   link whether it should be linked.

Note that these behaviours can be changed using options, see below.

You can also specify the page to work on directly, using "interwiki.py
pagename". But there are more possibilities, see below.

Working on more than one page
-----------------------------

Using the `XML Export <XML Export>`__, the pywikipediabot-software can
get more pages at once, upto 60 at a time. To use this possibility, you
can use the bot on a set of pages. The most common form is getting pages
in alphabetical order from Special:Allpages, using the -start option.

-start
~~~~~~

If you add the option -start, the bot will go through the pages
alphabetically, starting at the word specified. If you want to start at
the letter B, for example, you can use "interwiki.py -start:B". In
particular, if you want to do the whole Wiki, you can use "interwiki.py
-start:!"

Restarting: -continue, -restore
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Going through the whole wiki can, in large or even moderately large
wikis, take a long time. Thus, it may well happen that you are forced to
end the program before it has finished. In that case you can use
"interwiki.py -continue" next time. The bot, when it crashes or is
stopped (through control-c), will make a file specifying the pages it is
working on. If you use the continue-option, it will continue with those
pages, and after that continue alphabetically. If you want to restart a
non-alphabetical run, you can use "interwiki.py -restore" instead. It
will just restart the pages it was working on.

Be warned that only the **last** bot run that was stopped will be
recoverable. The bot will save its information to a file interwiki.dump,
and if another run is broken off, even if it is only on one page, it
will overwrite the file.

Autonomous mode
~~~~~~~~~~~~~~~

When working on a lot of pages, you may want the bot to just continue,
rather than asking you every time it sees a problem. This is done by
adding the option "-autonomous". If this option is used, the bot will
skip all problems and removals, and save a log of those in
``autonomous_problems.dat``. If you want it to do removals as well, add
the "-force" option too; in that case it is good to check the removals
afterward (often a page is removed because of a correctable typo).

The file sax\_parse\_bug.dat
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sometimes there is an error message mentioning a file
``sax_parse_bug.dat`` on the screen while running interwiki.py, and then
it starts retrieving some pages one-by-one instead of in a single batch.
This is caused by an illegal character in one of the pages to be
retrieved.

The tool ``xmltest.py`` can be used to trace this problem. Run it with
the filename as argument:

.. raw:: html

   <table bgcolor="#ffffcc">

.. raw:: html

   <tr>

.. raw:: html

   <td>

::

    python xmltest.py sax_parse_bug.dat

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

This will generate a python stack trace. The last line of that stack
trace will show a line number and column where the illegal character is
in the file. Please check this position, and if possible, correct the
wiki page associated with it.

Running on years AD
~~~~~~~~~~~~~~~~~~~

There is a special option **-years** that makes sure not to follow links
to centuries and decennia that are common on some wikipedias (like ja:).
Even then, this option should be used in combination with an exceptions
file (see below) because the la: and ia: number pages are about the
numbers and not about the years.

.. raw:: html

   <table bgcolor="#ffffcc">

.. raw:: html

   <tr>

.. raw:: html

   <td>

::

    python interwiki.py -autonomous -years

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

This will take a while to start up while it is preparing hints for all
pages named [[1]] through [[2050]]

If you stop the robot during a -years run and want to restart it later,
you can tell the robot at which page to restart by using **-years:XYZ**
where XYZ is the year where the robot stopped last time. You can also
make the robot start B.C. by making XYZ a negative number.

.. raw:: html

   <table bgcolor="#ffffcc">

.. raw:: html

   <tr>

.. raw:: html

   <td>

::

    python interwiki.py -autonomous -years:-500

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

Running on a simple list of pages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sometimes you have a list of pages available. Just a file of subjects,
each subject on a separate line, formatted as [[xx:yyy]] comments. The
**-file** option can be used to run the interwiki bot over such a list
of subjects. An example of such a file could be an
``autonomous_problems.dat`` file that you want to treat manually:

.. raw:: html

   <table bgcolor="#ffffcc">

.. raw:: html

   <tr>

.. raw:: html

   <td>

::

    python interwiki.py -file:autonomous_problems.dat

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

Using hints
-----------

Up to now, we have only worked on adding interwikis on pages that
already have some. But the bot can also be used to add them on pages
that have none yet. This is done by using hints. If for example you want
to add interwikis to the page [[en:House]], and think there might be a
page at [[fr:Maison]] that would be about the same subject, you can type
(if your bot is set to run on English by default) "interwiki.py House
-hint:fr:Maison".

If the link is to the same title, you can remove the title, and even the
second :. Also, if you want to link to the same word in several
languages, you can combine them with commas. So instead of "interwiki.py
Albert Einstein -hint:de:Albert\_Einstein -hint:fr:Albert\_Einstein
-hint:id:Albert\_Einstein" (those underscores are necessary, otherwise
the bot will disregard the 'Einstein' part of the pagename), you can
write "interwiki.py Albert Einstein -hint:de,fr,id",

Special hints
~~~~~~~~~~~~~

Some special hints have been defined to do a number of languages at
once. You can use them instead of the language part of a hint. Currently
the following special hints exist:

-  10: Ten of the largest projects of the family
-  20,30,50: Idem, for twenty, thirty and fifty languages
-  all: All projects with at least ~100 articles
-  cyril: All languages in Cyrillic script

The same are defined for Wiktionary, but at the moment of writing, 30,
50 and all are the same for Wiktionary. It is intended to add more
options.

Asking for hints
~~~~~~~~~~~~~~~~

When working on multiple pages such hints in the command line are rarely
useful. In that case (or if you want to decide on the hints later), you
can use the options "-askhints", "-untranslated" and
"-untranslatedonly". If you choose the -askhints option, for each page
you will be asked for one or more hints. They can be like the hints
after -hint: on the command line, but the ':' may not be omitted, and
spaces are allowed. Thus, valid hints would for example be "en:John
Smith", "de,nds,af:" or "50:". "-untranslated" asks for hints only if
there are no interwiki links yet; "-untranslatedonly" is like
-untranslated, but other pages are not worked on at all.

Instead of giving a hint, you can give an empty line. This specifies
that all hints for this page have been given (or that you have no hints
for it). Note that if you have given a hint, the bot will keep asking
for more hints until you press enter. Another option is to input a
question mark and nothing else; in that case you get shown the beginning
of the text to the page. If after that you input the question mark
again, it will give a larger part of the text, etcetera.

It might in these cases be useful to have the "-confirm" option added,
so the bot gets interactive before making a change. This can be used to
check whether the links are correct and/or as an impetus to create a
backlink.

Interaction of options
~~~~~~~~~~~~~~~~~~~~~~

If you've set ``without_interwiki = True`` in your
`user-config.py <Special:MyLanguage/Manual:Pywikibot/user-config.py>`__,
you may have generated a list of pages without interwikis from a
previous run of interwiki.py (you can use
`splitwithout.py <botwiki:Python:Splitwithout.py>`__ to split the list
and get lists for each individual language). In that case, you can use
the ``-file`` option to work directly on those pages, instead of
querying the database to find them. You can't (and don't need to) use
``-untranslated`` and ``-untranslatedonly`` with ``-file:``.

If you give a hint to a language, even if automatically with
``-hint:10,20,30,..,all`` (and also ``-same`` which works like
``-hint:all``), the option to ``-neverlink:`` that language won't work.
If you want to ignore that language, you have to remove it from the
family file or to give hints to all languages except that one
explicitly.

Wiktionary
~~~~~~~~~~

For Wiktionary articles there is the special "-wiktionary" option. It
works like "-hint:all", but has some extras because on Wiktionary some
languages use capitalisation and others don't, and links to another word
are never correct.

On non-capitalising wiktionaries, links to capitalising wiktionaries are
only added for capitalised words. Also, any link found to a word that
differs more than just in capitalisation, is ignored completely.

Automatic translation
---------------------

For years (both AD and BC) and days of the year, the bot can
automatically translate it in a large number of languages. If you do not
want this automatic translation (for example because it takes long to go
over such a large number of languages), it can be switched off with the
"-noauto" option.

With the option "-years:" followed by a number (positive or negative),
the bot goes through the years from the given year to 2050. If "-years"
without any addition is given, the beginning year is taken to be the
year 1.

With the option "-days" the bot goes through the days of the year;
however, this bot only works correctly on nl:.

Avoiding unwanted links
-----------------------

If you want to run the bot, but know that for a given page, it will get
to links that it should not get, you can use the -noredirect or
-neverlink or -select or -ignore options.

-noredirect means that if a redirect page is found, the redirect is not
followed, as is the normal behaviour, but the page is skipped.

-neverlink:xx with xx: a language code means that **any** links to the
language xx: are ignored.

-select lets you select or deselect every single links that is being
found individually, before any page is changed.

-ignore:zxx:pagetitle excludes the page named "pagetitle" in language
"zxx" and its interwiki links from inclusion, even if there are
interwiki links pointing to it.

Working with the logfile
------------------------

Each run of the ``interwiki.py`` program will write not only to the
screen, but also to a file called ``logs/interwiki.log``. You may have
seen that once a subject is completed, a list of *other* Wikipedias
interwiki links is printed preceded by 'WARNING:'. To use these lines,
the ``interwiki.log`` file is more convenient than the screen.

.. figure:: Interwiki.GIF
   :alt: Changing interwiki links to mr: wiki

   Changing interwiki links to mr: wiki
First an explanation why this is important. Assume you have a page [[My
Subject]] that links to [[fr:Mon Sujet]] and [[nl:Mijn Onderwerp]].
Assume also that neither the nl: nor the fr: page list your en: page:
they only know each other. A run of ``interwiki.py`` on either fr: or
nl: will not find your en: page. This can be referred to as *the
backlink problem*: there can be an *unknown* language that link to the
others, but as long as none of the others link back, there is no way of
discovering the existance. Do we really need to add these *back*\ links
manually? No, that is where the warnings come in. In the
``interwiki.log``:

.. raw:: html

   <table bgcolor="#ffffcc">

.. raw:: html

   <tr>

.. raw:: html

   <td>

::

    WARNING: fr:[[Mon Sujet]] does not link to [[en:My Subject]]
    WARNING: nl:[[Mijn Onderwerp]] does not link to [[en:My Subject]]

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

If the person running ``interwiki.py`` either on fr: or on nl: would
have this information, that would be sufficient to get the network of
links completed.

For this reason there is another option for the ``interwiki.py``
program:

.. raw:: html

   <table bgcolor="#ffffcc">

.. raw:: html

   <tr>

.. raw:: html

   <td>

::

    python interwiki.py -warnfile:english_treelang.log

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

In this mode the program will read the warnfile, and start to process
all of the pages that are mentioned for its home language using the
"does not link to" lines as hints. Some of those are uncontroversial and
can still be made automatically with the ``-autonomous`` option to
reduce manual work.

This process can still take a long time. If you trust the operator that
sent you the log, and the log is recent, you can also do:

.. raw:: html

   <table bgcolor="#ffffcc">

.. raw:: html

   <tr>

.. raw:: html

   <td>

::

    python warnfile.py english_treelang.log

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

This will not verify any of the suggestions in the warnfile, but blindly
implement them at full speed, saving the Wikipedia server a lot of
efforts.

Now, instead of sending the whole ``interwiki.log`` file to everyone,
there is a special program to split it up:

.. raw:: html

   <table bgcolor="#ffffcc">

.. raw:: html

   <tr>

.. raw:: html

   <td>

::

    python splitwarning.py

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

This will read your interwiki.log and create files called
``warning_XX.log`` (one for each language) that are more convenient to
use. If you zip these files up and make them available somewhere on the
internet, you can announce this at `Interwiki
bot/Warnfiles <Interwiki bot/Warnfiles>`__.

Overview of the options
-----------------------

Here is a list of the options, with an explanation of those that have
not yet been discussed.

-  **-array:** (usage: "-array:nn" with nn a number) When working on
   several pages, make sure to have at least this number of pages the
   bot is working on, if possible. The default value is 60; when using
   -untranslatedonly or a similar option, you might want to set it
   lower.
-  **-always:** Always save the page, even if only one byte has changed
   (default: save the page only if at least one link has actually
   changed)
-  **-askhints:** Ask hints (see above)
-  **-async:** Puts the page on a queue to be saved to wiki
   asynchronously. This enables loading pages during saving throtteling
   and gives a better performance.
-  **-autonomous** Work in autonomous mode (see above)
-  **-cleanup:** When an interwiki link is to be removed, just do it,
   don't ask for permission. This works like -force except keeping
   disambiguation mismatch and namespace mismatch unchanged.
-  **-confirm** Always ask permission before changing a page.
-  **-select** Ask for each link whether it should be include before
   changing any page.
-  **-days:** Work on the days
-  **-file:** (usage: "-file:filename") Specifies a file containing a
   list of pages to process. (Page names are specified as
   [[project:lang:pagename]], [[lang:pagename]], or [[pagename]].
-  **-force:** When an interwiki link is to be removed, just do it,
   don't ask for permission
-  **-hint:** Give a hint (see above)
-  **-name:** Old option; equivalent to "-hint:all", but capitalizes the
   last word when trying on eo:. Might get deprecated.
-  **-namespace:** Number or name of namespace to process. Can be used
   multiple times. Do not use with the -start parameter (use something
   like -start:Category:! instead)
-  **-neverlink:** Do not link to a specific language (see above)
-  **-noauto:** Do not use automatic translation (see above)
-  **-nobacklink:** Do not give a list of missing links on pages linked
   to
-  **-nobell:** Give no audio sign when asking for input.
-  **-noredirect:** If the bot finds a page linked to is a redirect, it
   is skipped (normal behaviour: It follows the redirect)
-  **-noshownew:** Do not show new links found
-  **-number:** (usage"-number:nn" with nn a number) In combination with
   -start, checks only the first nn pages rather than the whole wiki.
-  **-same:** Old option; equivalent to "-hint:all"; might get
   deprecated
-  **-showpage:** When using -askhints or some such option, always show
   the page text, even if not prompted.
-  **-skipfile:** (usage "-skipfile:filename") On a run using -start, do
   not do the pages in the file start
-  **-untranslated:** Ask hints for untranslated pages (see above)
-  **-untranslatedonly:** Ask hints for untranslated pages (see above)
-  **-warnfile:** Use the logfile for pages and hints (see above)
-  **-wiktionary:** Special wiktionary options (see above)
-  **-years:** Work on the years

.. raw:: mediawiki

   {{Manual:Pywikipediabot/Global Options}}

See also
--------

-  `Using the python wikipediabot <Using the python wikipediabot>`__
-  `meta:Interwiki graphs <meta:Interwiki graphs>`__
-  botwiki:Python:Splitwithout.py

-  `Manual:Pywikipediabot/interwiki.py/Wiktionary functionality
   discussion <Manual:Pywikipediabot/interwiki.py/Wiktionary functionality discussion>`__
-  `Manual:Pywikipediabot/interwiki.py/Wiktionary functionality
   discussion/2007 <Manual:Pywikipediabot/interwiki.py/Wiktionary functionality discussion/2007>`__

`interwiki.py <category:Pywikibot scripts>`__
