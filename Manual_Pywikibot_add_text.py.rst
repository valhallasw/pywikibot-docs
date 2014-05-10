.. raw:: mediawiki

   {{Template:Pywikibot/Script  | core=y | compat=y }}

This is a script which helps to add a text **at the end** of the page
but above categories, interwiki and template for the stars of the
interwiki (default setting), or add a text **at the top** of the page.

This needs Python with at least v2.4 (not v2.3) as stated on `m:Using
the python wikipediabot <m:Using the python wikipediabot>`__.

Parameters
----------

These command line parameters can be used to specify which pages to work
on:

&params;

Furthermore, the following command line parameters are supported:

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;" >

::

    -cat                Targets entries within a specific category
    -page               Use a page as generator
    -text               Define which text to add
    -summary            Define the summary to use
    -except             Use a regex to check if the text is already in the page *
    -excepturl          Use the html page as text where you want to see if there's the text, not the wiki-page.
    -newimages          Add text in the new images
    -untagged           Add text in the images that don't have any license template
    -always             If used, the bot won't ask if it should add the text specified
    -up                 If used, put the text at the very top of the page *
    -file               Read a list of pages to treat from the named text file. Page titles in the file must be 
                        enclosed with [[brackets]] or separated by newlines. Argument can also be given as "-file:filename".

.. raw:: html

   </div>

For more command line parameters, run the bot help command for example:
``python add_text.py -help | more``

Example
-------

Adding a template to specific pages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It will add the text "{{Documentation subpage}}" at the very top of the
pages with "Category:Template documentation", except for those which
already include it.

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

add\_text.py -cat:template\_documentation -text:"{{Documentation
subpage}}" -except:"\\{\\{([Tt]emplate:\|)[Dd]ocumentation [Ss]ubpage"
-up

.. raw:: html

   </div>

-  ``-cat:template_documentation`` : only target entries categorized in
   the page of "Category:Template documentation"
-  ``-text:"<nowiki>{{Documentation subpage}}</nowiki>"`` : add the
   template "{{Documentation subpage}}" (excluding the quotes)

   -  To insert return code, use "\\n". But, if you use "-up" option, it
      becomes invalid.

-  ``-except:"\{\{([Tt]emplate:|)[Dd]ocumentation [Ss]ubpage"`` : regex
   commands to exclude entries which have this template already in the
   page
-  ``-up`` : Put the text at the top of the page instead

Another example:

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

python add\_text.py -cat:catname -summary:"Bot: Adding a template"
-text:"{{Something}}" -except:"\\{\\{([Tt]emplate:\|)[Ss]omething" -up

.. raw:: html

   </div>

Adding category to pages without any category
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This is a real instance that is used on it.wikipedia to put the template
in the page without any category, because if there are any hidden
categories, the page will be defined as categorized.

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

python add\_text.py -excepturl:"class='catlinks'>" -uncat
-text:"{{Categorizzare}}"
-except:"\\{\\{([Tt]emplate:\|)[Cc]ategorizzare" -summary:"Bot: Aggiungo
template Categorizzare"

.. raw:: html

   </div>

.. raw:: mediawiki

   {{Manual:Pywikipediabot/Global Options}}

`add text.py <Category:Pywikibot scripts>`__
