Copied from w:User:DumZiBoT/refLinks

What is  `doing <w:Special:Contributions/DumZiBoT>`__?
-----------------------------------------------------

He is converting bare external links in `references <w:WP:FOOT>`__ into
`named external
links <w:Wikipedia:How to edit a page#Links_and_URLs>`__.

Here are some examples of his work:
`1 <http://en.wikipedia.org/w/index.php?title=Argument_from_ignorance&diff=prev&oldid=188799228>`__,
`2 <http://en.wikipedia.org/w/index.php?title=Linus_Torvalds&diff=prev&oldid=188799140>`__,
`3 <http://en.wikipedia.org/w/index.php?title=Lithium&diff=prev&oldid=188799102>`__
and `here <w:Special:Contributions/DumZiBoT>`__ is what he is doing now.

He *usually* runs every time that a new `XML
dump <w:Wikipedia:Database download>`__ is available. Processing a dump
takes days : handling enwiki's March 15th dump took more than **120
hours**, 5 days of uninterrupted work.

His owner is `NicDumZ <w:User Talk:NicDumZ>`__.

The idea
--------

References like these:

-  ``<nowiki><ref>[http://www.google.fr]</ref></nowiki>``\  [1]_
-  ``<nowiki><ref>http://www.google.fr</ref></nowiki>``\  [2]_

are converted into this:

-  ``<nowiki><ref>[http://www.google.fr Google<!-- Bot generated title -->]</ref></nowiki>``\  [3]_

They look like this:

.. raw:: html

   <references/>

-  The title which is used as the url title is the HTML title from the
   linked page. (from the <title> tag)
-  newlines, linefeeds, and tabs from titles are converted into a single
   space to avoid long titles. Extra spaces are also removed.
-  Titles containing ], several consecutive } or ' are handled
   correctly, converting some of the preceding characters to their html
   entities (`This title enclose brackets
   [here] <http://example.org>`__)
-  When content-type is not ``text/html`` (medias, .doc, etc...), I
   can't automatically find a title, hence I only convert references to
   ``<nowiki><ref>http://lien.org/doc.pdf</ref></nowiki>``.
-  Lengthy titles are arbitrarily truncated to 250 characters. When this
   happens, "..." is appended to the title.

Features
~~~~~~~~

-  Reads the titles from PDF files
-  If a dead link is found, it is tagged using
-  When no <references/> or is in the page, <references/> is appended.
-  When duplicate references are found (i.e. references having the exact
   same content) only the first is kept, and a refname is added to the
   others (
   `example <http://fr.wikipedia.org/w/index.php?title=Utilisateur:NicDumZ/Test6&diff=prev&oldid=31118383>`__
   )

Hey, you forgot some links!
---------------------------

.. raw:: mediawiki

   {{ambox
   | style=background:#d9eaf6; border:1px solid #4682b4; border-left:10px solid #4682b4; color:#333333;
   | image = [[w:Image:Nuvola apps important.svg|50px]]
   | text = '''If a link is unchanged after an edit by DumZiBoT, please check that you can access the linked page.'''</br>
   <small>If you think that a particular link was ignored by DumZiBoT because it's ''particular'', please [[w:User talk:NicDumZ|poke me]].</small>
   }}

Some links may not be changed, even after DumZiBoT's run. These things
may have occurred :

-  The HTML linked page has no title (rare, but happens).
-  DumZiBoT got an HTTP error while trying to get the page (see `4xx
   Client Error <w:List of HTTP status codes#4xx_Client_Error>`__ and
   `5xx Client Error <w:List of HTTP status codes#5xx_Client_Error>`__).
   The link may be invalid, the page may not be available anymore, or
   may be protected. These links should be repaired or removed, but
   chances are that the error is temporary. Also, some pages, such as
   Google cache links, and Google books pages, give bots a 401/403 error
   although they're available. You may wish to try the `Link checker
   tool <w:User:Dispenser/Link checker>`__ to correct the problem.
-  Either the link or the html title is
   `blacklisted <w:blacklist#Computing>`__.

Blacklists
~~~~~~~~~~

-  *Link* **blacklist** : for now, only w:JSTOR links are ignored, since
   for non-registered users JSTOR gives the message: "JSTOR: Accessing
   JSTOR". Please `contact me <w:User talk:NicDumZ>`__ if you think that
   a particular domain should get blacklisted
-  *Title* **blacklist** : Based on an original idea from , I exclude
   links containing *register*, *sign up*, *404 not found*, and so on.

Meta-data
~~~~~~~~~

Why doesn't DumZiBoT include extra information, like access date,
author, or publication, or use `citation
templates <w:Wikipedia:Citation templates>`__? Changing the citation
style in an article `cannot be done without gaining
consensus <w:Wikipedia:Citing sources#Citation_templates>`__.
`SEWilcoBot <w:User:SEWilcoBot>`__ and `RefBot <w:User:RefBot>`__ were
blocked for changing the citation style in articles.

And what about server load?
---------------------------

The *search* for pages containing invalid references is made from the
last `XML dump <w:Wikipedia:Database download>`__. DumZiBoT only fetches
from the servers pages that *needed* modifications at the time of the
dump. (Some pages are downloaded but eventually do not need changes,
because the references were fixed between the dump and the fetch.)

Could you use  instead of the standard link syntax?
--------------------------------------------------

**No**. Read `this talk page
archive <w:User talk:NicDumZ/Archive 1#DumZiBoT>`__ for further
explanations.

Where do I request DumZiBoT to go through a specific page?
----------------------------------------------------------

Nowhere. Just wait : DumZiBoT goes through every page that need a fix
whenever a new dump is available.

Online tool
~~~~~~~~~~~

**However**, thanks to , you can manually run `DumZiBot's script on a
page <w:tools:~dispenser/cgi-bin/reflinks-svn.py>`__ or a `modified
script <w:tools:~dispenser/view/Reflinks>`__ which makes more
assumptions about references and formatting.

Where should I grumble report a problem?
----------------------------------------

-  `w:User Talk:NicDumZ <w:User Talk:NicDumZ>`__, and not elsewhere =)

Does DumZiBoT still make any edits?
-----------------------------------

No, DumZiBoT `has not edited since June
2009 <http://en.wikipedia.org/w/index.php?title=Special:Contributions/DumZiBoT&action=view>`__.

w:fr:Utilisateur:DumZiBoT/liensRefs

.. [1]
   `4 <http://www.google.fr>`__

.. [2]
   http://www.google.fr

.. [3]
   `Google <http://www.google.fr>`__
