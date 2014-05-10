Considerations when running Pywikibot under Windows
---------------------------------------------------

The Windows shell (cmd.exe) is less than perfect when it comes to
Unicode support. Because Pywikipediabot is used widely on non-English
MediaWiki sites, we support full Unicode output. However, you need to
change the font setting in cmd.exe before this works - or else you get a
lot of question marks!

Alternatively, Pywikipediabot also supports transliteration - for
instance, Вики is transliterated to Viki on Western European systems.
This also works without changing the font.

Because it is impossible to determine the font used, we ask that you
explicitly define which option you want to use. If you do not define
this, you will get the following warning:

::

    WARNING: Running on Windows and transliteration_target is not set.
    Please see http://www.mediawiki.org/wiki/Manual:Pywikipediabot/Windows

Full unicode output (suggested)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To get full unicode output, you need to change the font used by cmd.exe
and add a line to user-config.py.

Changing the font
'''''''''''''''''

#. Start cmd.exe or any pywikipedia script
#. Right-click on the icon in the top left corner ("C:\\") or left-click
   on the title bar
#. Go to 'Properties'
#. Go to the 'Fonts' tab
#. Select any font that has the TT-logo in front - on Windows XP, this
   is Lucida Console; on newer versions you can also choose Consolas.
#. Click 'OK'
#. Choose 'Save settings for all screens with the same title'

Your cmd.exe now is able to output full unicode!

Changing user-config.py
'''''''''''''''''''''''

To user-config.py, add the following line:

::

    transliteration_target = None

Blocks in output
''''''''''''''''

Because the font is unable to display all `glyphs <:en:glyphs>`__, you
will occasionally see characters like this: ☐. However, you can still
copy the text to visit the page on a wiki by copy-pasting the
characters.

If you'd rather have transliterated characters, please read on to the
following section.

Transliteration support
~~~~~~~~~~~~~~~~~~~~~~~

If you would like to have transliterated characters instead, you can add
the following like to user-config.py:

::

    transliteration_target = console_encoding

or, if you would like to transliterate back to only ascii characters,

::

    transliteration_target = 'ascii'

You can use any standard python encoding for this.

However, the output now is 'Viki' instead of 'Вики'. This means you
cannot copy-paste the page title anymore: `:ru:Viki <:ru:Viki>`__ is
\*not\* `:ru:Вики <:ru:Вики>`__!

`Windows <category:Pywikibot>`__
