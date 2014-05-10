This is a list of the existing bots with links to their descriptions.
Many of the red linked scripts with no pages are found in the Pywikibot
main folder. \_\_TOC\_\_

Global bot scripts
------------------

Editing scripts you are allowed to run on several wikis with a `global
bot flag <meta:Bot policy#Global_bots>`__.

Main bot scripts
----------------

.. raw:: mediawiki

   {{/part|
     {{/script|add_text|Adds text at the top or end of pages|y|y}}
     {{/script|category|Manages categories|y|y}}
     {{/script|imagecopy|Copies images from a wikimedia wiki to Commons|y|n}}
     {{/script|replace|Edits using text replacement|y|y}}
     {{/script|solve_disambiguation|Fixes disambiguation pages|y|y}}
     {{/script|table2wiki|Converts HTML tables to MediaWiki markup|y|n}}
     {{/script|upload|Uploads images to a wiki|y|y}}
     {{/script|weblinkchecker|Finds broken external links|y|y}}
   }}

Auxiliary programs
------------------

.. raw:: mediawiki

   {{/part|
     {{/script|clean_sandbox|This bot cleans a sandbox by replacing the current contents with predefined text.|y|y}}
     {{/script|cosmetic_changes|Makes the wiki source code look cleaner, invoked by other scripts|y|y}}
     {{/script|lonelypages|Place a template on pages which are not linked to by other pages, and are therefore [[Special:LonelyPages|lonely]]|y|y}}
     {{/script|selflink|Allows the operator to decide what to do about self links|y|n}}
     {{/script|transferbot|A script that transfers pages from a source wiki to a target wiki.|n|y}}
   }}

Other bot scripts
-----------------

.. raw:: mediawiki

   {{/part|
     {{/script|copyright|Checks for text violating copyright by looking for matches in search engines|y|n}}
     {{/script|standardize_interwiki|Moves interwiki links into standard locations|y|n}}
     {{/script|warnfile|creates backlinks from a interwiki.log file|y|n}}
     {{/script|welcome|Used to welcome new users|y|y}}
   }}

Change general pages
--------------------

.. raw:: mediawiki

   {{/part|
     {{/script|archivebot|Archives discussion threads|y|y}}
     {{/script|delete|Deletes pages ''en masse''|y|y}}
     {{/script|movepages|Moves page to another title|y|y}}
     {{/script|pagefromfile|Creates pages from a text file|y|y}}
     {{/script|standardize_notes|Refactors references and citations|y|n}}
   }}

Categories
----------

.. raw:: mediawiki

   {{/part|
     {{/script|catall|Adds or changes categories|y|y}}
     {{/script|category_redirect|Redirects pages etc. from one category to another.|y|y}}
     {{/script|catimages|Image by content categorization|y|n}}
     {{/script|cfd|This script processes the Categories for discussion working page.  It parses out the actions that need to be taken as a result of CFD discussions (as posted to the working page by an administrator) and performs them.|y|y}}
     {{/script|commons_category_redirect|This bot cleans [[Commons:Category:Non-empty category redirects]] by moving all the files, pages and categories from redirected category to the target category.|y|n}}
     {{/script|commonscat|Adds {{tl|commonscat}} to Wikipedia categories (or articles), if other language wikipedia already has such template|y|y}}
     {{/script|commons_link|Adds {{tl|commonscat}} and {{tl|commons}} to Wikipedia articles, if same name category or gallery exist on Commons.|y|y}}
     {{/script|imagerecat|Try to find categories for media on Commons|y|y}}
     {{/script|imageuncat|Program to add uncat template to images without categories at Commons.|y|y}}
     {{/script|makecat|Uses the links on a page to quickly populate a category|y|y}}
   }}

Images
------

.. raw:: mediawiki

   {{/part|
     {{/script|data_ingestion|A generic bot to do data ingestion (batch uploading) to Commons|y|y}}
     {{/script|delinker|Bot delinks and replaces images|y|n}}
     {{/script|flickrripper|upload images from [http://www.flickr.com Flickr] easily|y|y}}
     {{/script|imagecopy_self|Script to copy self published files from the English Wikipedia to Wikimedia Commons|y|n}}
     {{/script|imageharvest|Copies multiple images to a wiki|y|n}}
     {{/script|imagetransfer|Copies images to another wiki|y|y}}
     {{/script|image|Used to change one image to another or remove an image entirely.|y|y}}
     {{/script|inline_images|This bot goes over multiple pages of the home wiki, and looks for images that are linked inline (i.e., they are hosted from an external server and hotlinked, instead of using the wiki's upload function.|y|n}}
     {{/script|panoramiopicker|upload images from [http://www.panoramio.com Panoramio] easily|y|n}}
     {{/script|tag_nowcommons|Script tags files available at Commons with the Nowcommons template.|y|n}}
     {{/script|unusedfiles|Finds unused media using [[Special:Unusedimages]].|y|y}}
   }}

IRC scripts
-----------

`IRC <:w:IRC>`__ (Internet Relay Chat) Bots, all using the ``irclib``,
you `can download it on Bitbucket <https://bitbucket.org/jaraco/irc>`__.
All scripts are experimental state.

Page protection
---------------

.. raw:: mediawiki

   {{/part|
     {{/script|blockpageschecker|Deletes any protection templates that are on pages which aren't actually protected. |y|y}}
     {{/script|protect|Protect and unprotect pages en masse.|y|y}}
   }}

Templates
---------

.. raw:: mediawiki

   {{/part|
     {{/script|template|Replaces one template with another, in a way that is easier to use than [[../replace.py/]] in most instances|y|y}}
     {{/script|templatecount| Counts or lists the instances where templates are used|y|n}}
   }}

Wikidata
--------

.. raw:: mediawiki

   {{/part|
     {{/script|claimit|A script to mass add Wikidata claims to a lot of items based on pages on Wikipedia|n|y}}
     {{/script|coordinate_import|A script to mass import coordinates from Wikipedia to Wikidata|n|y}}
     {{/script|freebasemappingupload|A script to upload the mappings of Freebase to Wikidata|n|y}}
     {{/script|harvest_template|A script to mass add Wikidata claims based on information harvested from Wikipedia templates.|y|y}}
     {{/script|illustrate_wikidata|A script to add images to Wikidata items.|n|y}}
     {{/script|newitem|A script to mass create new Wikidata items.|n|y}}
   }}

Unsorted scripts
----------------

.. raw:: mediawiki

   {{/part|
     {{/script|capitalize_redirects|Bot to create capitalized redirects where the first character of the first word is uppercase and the remaining characters and words are lowercase.|y|n}}
     {{/script|casechecker| Script to enumerate all pages on the wiki and find all titles with mixed latin and cyrilic alphabets.|y|y}}
     {{/script|censure|Bad word checker bot|y|n}}
     {{/script|checkimages|Script to check recently uploaded files. This script checks if a file description is present and if there are other problems in the image's description.|y|y}}
     {{/script|copyright_clean||y|n}}
     {{/script|copyright_put||y|n}}
     {{/script|create_categories|Program to batch create categories.|y|y}}
     {{/script|daemonize||y|n}}
     {{/script|deledpimage||y|n}}
     {{/script|disambredir|Goes through the disambiguation pages, checks their links, and asks for each link that goes to a redirect page whether it should be replaced.|y|y}}
     {{/script|diskcache||y|n}}
     {{/script|djvutext|Extracts OCR text from djvu files and uploads onto pages in the "Page" namespace on Wikisource.|y|n}}
     {{/script|editarticle|Edit a Wikipedia article with your favourite editor.|y|y}}
     {{/script|extract_wikilinks||y|n}}
     {{/script|featured||y|y}}
     {{/script|fixing_redirects||y|y}}
     {{/script|followlive||y|n}}
     {{/script|gui|A TKinter window with a unicode text field where the user can e.g. edit the contents of an article.|y|n}}
     {{/script|interwiki_graph||y|n}}
     {{/script|isbn|This script goes over multiple pages of the home wiki, and reports invalid ISBN numbers, converts to ISBN-13 from ISBN-10 and places hyphens.|y|y}}
     {{/script|match_images||y|n}}
     {{/script|misspelling||y|y}}
     {{/script|ndashredir|Collect articles that have n dash or m dash character in their title and create a redirect to them from the corresponding hyphenated title|y|n}}
     {{/script|noreferences|Adds missing <nowiki><references /></nowiki> tag and references section if needed|y|y}}
     {{/script|nowcommons||y|y}}
     {{/script|overcat_simple_filter|A bot script to do some simple over categorization filtering.|y|n}}
     {{/script|pageimport||y|n}}
     {{/script|parserfunctioncount|This script helps to find expensive templates that are subject to be converted to Lua.|y|n}}
     {{/script|patrol|This script obtains a list of recentchanges and newpages and marks the edits as patrolled based on a whitelist.|y|n}}
     {{/script|piper|This is a bot that uses external filtering programs to munge the article text.|y|n}}
     {{/script|rcsort|cgi script|y|n}}
     {{/script|reflinks|A bot adding the title of linked web pages to bare external links; see [[w:en:User:DumZiBoT/refLinks]] by the original owner, cf. [[Archived Pages]].|y|y}}
     {{/script|replicate_wiki|This bot replicates all pages (from specific namespaces) in a wiki to a second wiki within one family.|y|y}}
     {{/script|revertbot||y|y}}
     {{/script|saveHTML||y|n}}
     {{/script|script_wui|Robot which runs python framework scripts as (sub-)bot and provides a
   WikiUserInterface (WUI) with Lua support for bot operators.|n|y}}
     {{/script|spamremove||y|y}}
     {{/script|speedy_delete||y|n}}
     {{/script|spellcheck||y|n}}
     {{/script|statistics_in_wikitable||y|n}}
     {{/script|subster|Script which does substitutions of tags within wiki page content with external or other wiki text data|y|n}}
     {{/script|sum_disc|This cript is used for summarize discussions spread over the whole wiki including all namespaces|y|n}}
     {{/script|titletranslate||y|n}}
     {{/script|udp-log||y|n}}
     {{/script|unlink||y|n}}
     {{/script|us-states|Check pages on the English Wikipedia whether they are in the form "Something, State", and if so, create a redirect from "Something, ST".|y|n}}
     {{/script|watchlist|Access the bot account's [[Special:Watchlist|Watchlist]].|y|n}}
     {{/script|wikicomserver||y|n}}
     {{/script|wikipediatools||y|n}}
     {{/script|wiktionary||y|n}}
   }}

Non editing scripts
-------------------

Scripts which do not change wiki pages. So are allowed on virtually all
wikis to run them.

Other scripts
-------------

Mostly internal scripts. No normal bots.

External links
--------------

-  `Pywikibot package
   content <https://git.wikimedia.org/tree/pywikibot%2Fcompat.git>`__ of
   compat branch
-  `Pywikibot package
   content <https://git.wikimedia.org/tree/pywikibot%2Fcore.git>`__ of
   core branch
-  botwiki:Template:Script#Script *(most outdated)* - long list of other
   scripts which are not (yet) part of the framework.

` <Category:Pywikibot scripts>`__ `Scripts <Category:Pywikibot>`__
