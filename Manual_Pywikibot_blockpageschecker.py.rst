 `blockpageschecker.py <category:Pywikibot scripts>`__
**blockpageschecker.py** is a pywikipedia script which solves a problem
that afflicts many wikis. It finds pages which are currently displaying
a template that says the page is being
`protected <help:protected pages>`__ in some way, and then checks to see
if it actually **is** protected. If the page is not genuinely protected,
it will prompt the user to remove the protection template.

Unlike many pywikipedia scripts that are a part of the standard
complement of scripts, however, this one doesn't work on *any* English
language wiki straight out of the box. You *must* `tailor the raw code
to your particular wiki <#Customising_the_code>`__ to get it to work.
Once you've done so, though, operation is genuinely easy.

Concept
-------

When administrators want to restrict the editing of a page, they will
`protect <help:protected pages>`__ it in some way. They might prevent a
page from being moved (renamed). Or they might restrict editing rights
to only registered users. Or they might prevent anyone but
administrators having anything to do with it.

Many wikis have created protection templates, which alert readers about
the protected status of the page.

However, these templates sometimes get abused by non-administrators, who
wish to "warn off" other users from editing a page. Or sometimes
administrators place a temporary editing ban on a page, but then forget
to return to the page to remove the template after the protection
expires.

Whatever the reason, there are, on almost every wiki where
administrators care about page protection, some pages which *claim* to
be protected, when they actually aren't.

This script finds the pages that have a protection template, then checks
to see whether the page is actually protected in the way the template
suggests. If it isn't, it signals the operator to delete the template.

Syntax
------

Syntax is fairly straightforward. Just type:

    ``python blockpageschecker.py ''-parameter1'' ''parameter2'' . . . ''parameter3''``

Although the script can be run without parameters — in which case it
will check the categories which are defined by the script's raw code
— it also accepts a number of command line parameters. These include:

::

    -xml              Retrieve information from a local XML dump (pages-articles
                      or pages-meta-current, see http://download.wikimedia.org).
                      Argument can also be given as "-xml:filename".

    -page             Only edit a specific page.
                      Argument can also be given as "-page:pagetitle". You can
                      give this parameter multiple times to edit multiple pages.

    -protectedpages:  Check all the blocked pages; useful when you don't have
                      categories or when you have problems with them. (add the
                      namespace after ":" where you want to check - default checks
                      all protected pages.)

    -moveprotected:   Same as -protectedpages, for moveprotected pages

    Furthermore, the following command line parameters are supported:

    -always         Doesn't ask every time if the bot should make the change or not,
                    do it always.

    -show           When the bot can't delete the template from the page (wrong
                    regex or something like that) it will ask you if it should show
                    the page on your browser.
                    (attention: pages included may give false positives!)

    -move           The bot will check if the page is blocked also for the move
                    option, not only for edit

Usage
-----

The easiest way to use this script is to take the time to alter the raw
code of the script so that it looks for what you want to find on your
own wiki. Indeed the script **will not work** on any English language
wiki with just command line instructions (like
``python blockpageschecker.py``) *unless* you take the time to open it
up in an editor and change the base code. Once you've made the
appropriate settings in the code, operation becomes totally painless. If
you've set up your code correctly — and it really is fairly
straightforward! — the *only* way you'll need to use this script is to
type

    ``python blockpageschecker.py``

That's it! You won't need a single parameter.

However, if you wish to add any of the parameters suggested above, then
you can add them, one right after the other, like:

    ``python blockpageschecker.py -cat:"Popular templates" -always``

Customising the code
--------------------

Because the code "ships" with English language options set to "none", it
won't work on English language wikis without modification of the code.
Fortunately, the code is very well annotated, and has examples of
syntactically correct setups in other languages.

All you have to do is navigate to ``blockpageschecker.py`` in your
``pywikipedia`` folder, open it, then take a few moments to read through
the code carefully. The default on most code editors is that
instructions are given in red. Pay special attention to these sections.

What you're particularly looking for is a section called "preferences".

Customise templates to look for
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section allows you to tell the script what the names of your
protection templates are. Most wikis have at least a total protection
and a semi-protection template. Figure out what yours are, and put them
in there. You'll note, however, that it's expecting the name of the
template to be given in terms of a `regular
expression <wikipedia:regular expression>`__. This kind of coding may be
unfamiliar to some, so here's a good example to use:

    ``'en': [ur'\{\{(?:[Tt]emplate:|[Pp]rotect)\}\}'],``

This will find , even if it appears as on pages. Change this to be
whatever the name of your template, making sure that the first letter of
the template name is given with upper and lower case. For instance, if
your template is called , then change ``[Pp]rotect`` to ``[Ll]ockdown``.
Make sure you change *nothing* else about the code snippet, however.
Even a missing comma or an extra space can introduce a syntax error.

Note, however, that the example above only works for templates that
accept no variables, and one where there are no spaces between the curly
braces and the word *protect*. If you have a protection template which
uses variables, such as ``{{tl|Protect|2}}`` then it won't work to just
look for ``{{tl|Protect}}``. You'll need to do a more complicated
regular expression (regex) to account for the fact that variables are
possible. Luckily, the code has some examples built in. Examine what's
happening on the French and Italian lines, for instance.

Put another way, the example above works in a lot of cases, but it does
make assumptions that might not apply to your particular wiki.

Example
^^^^^^^

On the French Wikipedia by default the script displays: *WARNING: No
edit-protection template could be found*, because it didn't searched for
{{SP}}.

The solution was to add into ``blockpageschecker.py`` line 86:

``'fr': [ur'\{\{(?:[Tt]emplate:|[Mm]odèle:|)(?:[Ss]P)(|[^\}]*)\}\}'],``

and to relaunch
``python blockpageschecker.py -lang:fr -family:wikipedia``.

Customise categories to search in
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After you've changed the templates, you then need to scroll down at
change the ``categoryToCheck`` variable. Again, you'll go to the line
marked ``'en'``, if you're on an English language wiki. Change the
category to whatever category is appropriate for your wiki. Generally
protection templates automatically put pages into a category (and if
they don't, they should be altered to do this). If you then tell the bot
to look in all the categories that are generated by the protection
template(s), you'll be able to check your wiki for invalid tags most
easily. Take the time to change the category here in the base code and
you'll be able to type *only* ``python blockpageschecker.py`` to
*completely* check your wiki. It'll reduce your maintenance time to a
matter of seconds.

Customise other things
~~~~~~~~~~~~~~~~~~~~~~

There are a few other buttons you can push in the preferences section,
but there are none others that you *need* to set in order to get the
script to run. Look through the list to see if there are any other
changes that might work for you.
