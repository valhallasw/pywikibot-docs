 **User-fixes.py** adds some custom fixes to the Pywikipediabot text
replacement utility, `replace.py <Manual:Pywikipediabot/replace.py>`__.
It is created by running
``[[Manual:Pywikipediabot/generate_user_files.py|generate_user_files.py]]``
if it doesn't already exist. To call your fixes you use
`replace.py <Manual:Pywikipediabot/replace.py>`__.

User-fixes.py is very similar to **fixes.py**. For detailed explanation
and comparison, see Manual:Pywikipediabot/fixes.py.

Example
-------

To call your fixes:

.. code:: bash

    python replace.py -fix:example -page:MainPage

Which looks for 'example' in user-fixes.py, and applies the fixes to the
main page.

When first created, User-fixes.py looks like this:

.. code:: php

    # -*- coding: utf-8  -*-

    #
    # This is only an example. Don't use it.
    #

    fixes['example'] = {
        'regex': True,
        'msg': {
            '_default':u'no summary specified',
        },
        'replacements': [
            (ur'\bword\b', u'two words'),
        ]
    }

Modified file:

.. code:: php

    # -*- coding: utf-8  -*-

    #
    # This is only an example. Don't use it.
    #

    fixes['example'] = {
        'regex': True,
        'msg': {
            '_default':u'no summary specified',
        },
        'replacements': [
            (ur'\bword\b', u'two words'),
        ]
    }

    #
    # Add wikilinks. 
    # This fix is used with command:
    # python replace.py -fix:wikilinks [-nocase] -subcat (or -xml)

    fixes['wikilinks'] = {
        'regex': True,
        'msg': { '_default':u'adding wikilinks', },
        'replacements': [
            (r'(?i)\b(barrettes)', r"[[\1]]"), # barrettes will be changed to [[barrettes]]
            (r'(?i)\b(barrette)', r"[[\1]]"),       
        ]
    }

Advanced use of fixes
~~~~~~~~~~~~~~~~~~~~~

To learn how to use your own functions in fixes.py and user-fixes.py and
what this is good for, see `:hu:Szerkesztő:Bináris/Fixes and functions
HOWTO <:hu:Szerkesztő:Bináris/Fixes and functions HOWTO>`__.

See also
--------

-  `Using the python wikipediabot <Using the python wikipediabot>`__

`Category:Pywikibot user scripts <Category:Pywikibot user scripts>`__
