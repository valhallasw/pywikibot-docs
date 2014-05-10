.. raw:: mediawiki

   {{MoveToMediaWiki}}

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/interwiki.py/Wiktionary functionality discussion}}

.. raw:: mediawiki

   {{shortcut|WM:IW-WIKT}}

For the previous version of this page/discussion see `/2007 </2007>`__.

This is a discussion of how interwiki language links work and should
work in the Wiktionaries. Note that most of this applies only to
namespace 0, the main namespace; the other namespaces are done much as
the 'pedia and other projects do.

Maintaining ``interwiki.py``
----------------------------

There are serious issues with maintenance of ``interwiki.py`` for
"wiktionary mode": problem and bug reports go unanswered and unfixed for
weeks and months, while operators believe that by re-syncing nightly
they are up to date. In a few cases, the maintainers have refused to
make necessary corrections (thus, for example, the program is un-usable
on the pl.wikt).

+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| width=20% \| issue                       | width=20% \| status on sourceforge                                                                                                                                                                     | comments                                                                                                                                                                                                                                                                                                                 |
+==========================================+========================================================================================================================================================================================================+==========================================================================================================================================================================================================================================================================================================================+
| not add links to specific other wikt     | refused to fix `1 <http://sourceforge.net/tracker/?func=detail&aid=2531705&group_id=93107&atid=603141>`__ `2 <http://sourceforge.net/tracker/?func=detail&aid=2531527&group_id=93107&atid=603141>`__   | The Polish wikt does not allow standard bots to link to the Russian wiktionary; the problem is that many of the entries there are empty templates. It is not that they don't link to ru.wikt, it is that the links are added by their own program (Tsca.bot) which checks in some way, other bots should not add them.   |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| wikts using alpha-by-name revised sort   | was pending `3 <http://sourceforge.net/tracker/?func=detail&aid=2605385&group_id=93107&atid=603138>`__, closed without being fixed after a year                                                        | Some wikts want the sort order to be the "revised" order used by some 'pedias.                                                                                                                                                                                                                                           |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| sv.wikt wants "Dodde order"              | claimed fixed `4 <http://sourceforge.net/tracker/?func=detail&aid=2023095&group_id=93107&atid=603138>`__, but was not                                                                                  | particular sort order designed originally for the Swedish Wiktionary.                                                                                                                                                                                                                                                    |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| linking to redirects                     | apparently refused (tbc, no tracker link found)                                                                                                                                                        | See below, a serious problem as the existing code will remove links, and thus cannot be run on some wikts.                                                                                                                                                                                                               |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Sort order
----------

Keeping the "framework" code up to date is a crock, and proves very hard
to maintain. This is also true for other projects.

It has been suggested that the sort order be specified in a Mediawiki:
namespace message for each project, defaulting to code order. This would
be vey useful.

At present, the order in the framework is incorrect for da, ms, and sv;
and possibly others.

Linking to redirects
--------------------

It has been the default policy, as implemented in ``interwiki.py``, not
to add links to the same form on another wikt when the target of the
link is a redirect.

It is not clear whether this was ever intentional, or a side-effect of
the hacking of the wikipedia interwiki code to operate in "wiktionary
mode".

It would be much more useful to have a standard policy of always linking
to redirects in the other wikt.

Note: At this time, Interwicket only adds links to redirects when it is
configured to for specific wikts; the others are treated as default: it
neither adds links to redirects nor removes them if found.

Idiom forms
~~~~~~~~~~~

Wikts often use different canonical forms for a given idiom, either in a
standard way or arbitrarily.

For example: `:en:fix und fertig <:en:fix und fertig>`__ and `:de:fix
und fertig sein <:de:fix und fertig sein>`__ are the entries. On the
en.wikt, `:en:fix und fertig sein <:en:fix und fertig sein>`__ is a
redirect to the entry, on de.wikt, `:en:fix und
fertig <:en:fix und fertig>`__ is a redirect. This works well with iwiki
links to redirects, but is broken without: en.wikt links to redirects,
de.wikt does not (table as of status 31 January 2009)

+-------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------+-------------------------------------------------------------------+
| user starts at                                                    | sees page                                                         | iwiki link                                              | arrives at                                                        |
+===================================================================+===================================================================+=========================================================+===================================================================+
| `:wikt:en:fix und fertig <:wikt:en:fix und fertig>`__             | `:wikt:en:fix und fertig <:wikt:en:fix und fertig>`__             | `:wikt:de:fix und fertig <:wikt:de:fix und fertig>`__   | `:wikt:de:fix und fertig sein <:wikt:de:fix und fertig sein>`__   |
+-------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------+-------------------------------------------------------------------+
| `:wikt:en:fix und fertig sein <:wikt:en:fix und fertig sein>`__   | `:wikt:en:fix und fertig <:wikt:en:fix und fertig>`__             | `:wikt:de:fix und fertig <:wikt:de:fix und fertig>`__   | `:wikt:de:fix und fertig sein <:wikt:de:fix und fertig sein>`__   |
+-------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------+-------------------------------------------------------------------+
| `:wikt:de:fix und fertig sein <:wikt:de:fix und fertig sein>`__   | `:wikt:de:fix und fertig sein <:wikt:de:fix und fertig sein>`__   | (none)                                                  | (can't get there)                                                 |
+-------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------+-------------------------------------------------------------------+
| `:wikt:de:fix und fertig <:wikt:de:fix und fertig>`__             | `:wikt:de:fix und fertig sein <:wikt:de:fix und fertig sein>`__   | (none)                                                  | (can't get there)                                                 |
+-------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------+-------------------------------------------------------------------+

If de.wikt allowed links to redirects, this would work exactly as it
should. And if either wikt (or any other language also linking these
titles) moves from one to the other (reverses redirect) it continues to
work correctly *without modifying the interwiki links*.

Typographical forms
~~~~~~~~~~~~~~~~~~~

Different wikts use various standard typography; the en.wikt uses a
straight apostrophe in (almost) all cases, while the fr.wikt uses
`’ <’>`__ ("right single quotation mark") in the same cases. So
`:wikt:en:z' <:wikt:en:z'>`__ is the standard form on en, and
`:wikt:fr:z’ <:wikt:fr:z’>`__ on the fr.wikt. Linking to the redirects,
`:wikt:en:z’ <:wikt:en:z’>`__ and `:wikt:fr:z' <:wikt:fr:z'>`__ provides
the reader with access to the standard form on the other wikt. (Note
that as of this writing, a user has added a non-standard iwiki to the
fr.wikt page ;-).

The issue here is linking to the redirects in both directions so the
entries can be found. (And *not* to try to impose the standard
apostrophe used on the other wikts.)

Character forms
~~~~~~~~~~~~~~~

The English wikt has entries for `:wikt:en:食 <:wikt:en:食>`__ (U+98DF)
and a modified form of the radical `:wikt:en:飠 <:wikt:en:飠>`__
(U+98E0), (radical 184), the zh wiktionary combines the entries, with
the form redirected to the radical. Likewise the simplified form
`:wikt:en:饣 <:wikt:en:饣>`__ is redirected to the traditional form. The
interwiki links from en.wikt all work correctly, as it links to these
redirects; other wikts that are not linking to redirects have no
interwiki links for these characters to the zh.wikt, a rather large
omission.

Inflected forms
~~~~~~~~~~~~~~~

For example, while the en.wikt has entries for
`:wikt:en:cerveza <:wikt:en:cerveza>`__ and
`:wikt:en:cervezas <:wikt:en:cervezas>`__, the ca.wikt (Catalan)
redirects `:ca:cervezas <:ca:cervezas>`__ to
`:ca:cerveza <:ca:cerveza>`__. A reader starting on the Catalan
wiktionary will always see `:wikt:ca:cerveza <:wikt:ca:cerveza>`__, and
iwiki to the singular form in the en.wikt (which of course has the
inflections linked in the text). A reader starting with the en.wikt will
see the form looked for; following the iwiki link for ca will arrive at
`:wikt:ca:cerveza <:wikt:ca:cerveza>`__ in either case.

The Bulgarian wiktionary also has a very large number of bot-generated
redirects to (presumably) a base form.

Vowel markings (Arabic, Hebrew, etc)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Different wikts have very different policies (or non-policies)
concerning redirects from forms to the "defective" form, without
markings. (Or to different markings.) Linking to the redirects is a best
effort case for getting the reader to the desired entries.

Capitalization
~~~~~~~~~~~~~~

There still are a number of redirects left over from the "conversion
script", although we've deleted most from en.wikt; most wikts had few or
no entries when the script was run. In any case, it is not harmful to
end up at a different capitalization on the other wikt; it may be the
desired form; the redirect may be intentional.

Odd cases
~~~~~~~~~

A number of other cases exist due to local policies and conventions. For
example `:wikt:ur:business <:wikt:ur:business>`__ redirects to the Urdu
word, rather than being an entry for the English word with the Urdu
definition. (It isn't clear whether this is policy, convention, or
mistake ...) So `:wikt:en:business <:wikt:en:business>`__ has a link to
the intended (?) entry in the Urdu wiktionary.

Some wikts use redirects for spelling variants or errors.

Move leftovers, junk
~~~~~~~~~~~~~~~~~~~~

Move leftovers from errors might be useful, but probably not; but will
only be linked to from an actual entry, so they are words in some
language. Pure junk (vandalism, etc) will exist whether redirects or
not, but if not words, there won't be any valid entries to link to them
anyway.

Summary
~~~~~~~

Linking to redirects in the other wikt is an all-around win, the
negatives are almost non-existent. We really should make the default
policy be linking to redirects; while still permitting wikts to have
specific policy (of course). However, it might be reasonable with the
appropriate community discussion to make linking to redirects universal
policy.

Main pages
----------

Depending on whether a wikt is mostly unused yet, somewhat developed, or
fully developed, the "main page" is found it several different states.
Sometimes it is still called "Main page". Often it is called something
language specific, but still in namespace 0. The Mediawiki: pointer may
or may not point directly to it, and it may or may not be protected.

Ideally, the main page will be in Project: space, with interlanguage
links as usual for that namespace (and all other non-zero namespaces on
the wikts). This is least confusing for interwiki bots. They may not be
able to update the page as it is usually protected, but will be able to
read it and use the information normally.

`interwiki.py/Wiktionary functionality
discussion <Category:Pywikibot scripts>`__
