.. raw:: mediawiki

   {{MoveToMediaWiki}}

Adapting scripts to translatewiki
---------------------------------

Sun Jan 16 13:33:11 UTC 2011

Hello all,

After my last mail, you have of course set up a working rewrite
development environment and were wondering how to spread TW integration
like a virus through the scripts/ directory. So, how to do it:

As you will notice, there is now a i18n/ directory inside the scripts/
directory. This directory contains all files exported from
TranslateWiki. The script name defines which TW keys are defined in the
file, so i18n/category.py contains category-\* (category-was-moved [1]_,
category-also-in, etc). These are the translations that before were in
scripts/category.py.

Adapting scripts to translatewiki consists of four parts:

| ``* Defining TW keys for translations``
| ``* Reading in translations and outputting them into the TW format``
| ``* Removing translations from script file``
| ``* Adding 'from pywikibot import i18n' and adapting all/most``
| ``  pywikibot.translate entries with i18n.twtranslate().``

-  (1) Defining TW keys\*

To use isbn.py as an example. There is only one message (only showing
german and english):

.. code:: python

    msg = {
       'de': 'Bot: Formatiere ISBN',
       'en': 'Robot: Formatting ISBN',
    }

For TW, we define this message as isbn-formatting.

Sometimes pywikibot.translate is used for site- or language-specific
configuration. Don't move those to translatewiki files (yet).

-  (2) Reading in translations and outputting them into the TW format\*

Although it is possible to do the isbn example by hand, I'll use a
script that can easily be adapted for a larger number of messages. Don't
forget to ``source bin/activate`` your virtualenv! The script is
available at http://pastebin.com/u2XrKt5b (too long to paste in this
e-mail)

For other scripts, you have to adapt at least lines 2, 6 and 12. Line 12
has a list of tuples (old dict, translatewiki key). If the messages have
(one or more) parameters, you should change them to \*named
parameters\*, so translators can move them around in the message. See
lines 15 and 16 for an example of how to do this.

Running this script gives you a new file, i18n/isbn.py

-  Test\* the translation:

::

    (pwbde)/rewrite/scripts$ python
    >>> from pywikibot import i18n
    >>> i18n.twtranslate("de", "isbn-formatting")
    u'Bot: Formatiere ISBN'

hurrah!

-  (3) Removing translations from the script file\*

Use a sledgehammer, jackhammer or scalpel. Whatever works for you. In
the case of isbn.py, lines 49 to 61.

-  (4a) Add from pywikibot import i18n\*

::

    -from pywikibot import pagegenerators
    +from pywikibot import pagegenerators, i18n

-  (4b) Adapting all/most pywikibot.translate entries\*

Search for pywikibot.translate. Change the following:

.. code:: python

    pywikibot.translate(site, msg) % (param_1, param_2)

to

.. code:: python

    i18n.twtranslate(site, "tw-key-for-msg", {'param_1': param_1, 'param_2': param_2})

or

.. code:: python

    i18n.twtranslate(site, "tw-key-for-msg") % {'param_1': param_1, 'param_2': param_2}

With \*'tw-key-for-msg'\* referring to the tw key you thought up for
\*msg\*, and \*'param\_1'\* and \*'param\_2'\* (the dictionary keys)
referring to the \*named parameters\* you introduced in step 2.

For isbn.py, this is simpler:

::

    -        self.comment = pywikibot.translate(pywikibot.getSite(), msg)
    +        self.comment = i18n.twtranslate(pywikibot.getSite(), 'isbn-formatting')

-  Congratulations! \*You have adapted a script to use translatewiki
   translations!

Of course, before committing, \*test\* the script:

::

    (pwb)/rewrite/scripts$ *python isbn.py -page:Gebruiker:Valhallasw -to13 -format*
    (...)
    Page [[Gebruiker:Valhallasw]] saved
    yielding:
    (huidig | vorige)  16 jan 2011 14:29 Valhallasw (Overleg | bijdragen) k (1.735 bytes) (Bot: ISBN opgemaakt) (ongedaan maken)

And, as a last step, \*commit\* the script (and the translations!) to
the svn repository: Special:Code/pywikipedia/8838

Good luck adapting scripts!

Best regards, `Valhallasw <User:Valhallasw>`__ 21:23, 11 July 2011 (UTC)

.. raw:: html

   <references />

See also
--------

-  http://thread.gmane.org/gmane.comp.python.pywikipediabot.general/12402/focus=12413

`I18n conversion <Category:Pywikibot>`__
`Pywikipedia <Category:Localisation>`__

.. [1]
   translatewiki:Pywikipedia:Category-was-moved/en
