.. raw:: mediawiki

   {{MoveToMediaWiki}}

.. raw:: mediawiki

   {{template:Pywikipediabot|script}}

**unusedfiles.py** is part of the `pywikipediabot <pywikipediabot>`__
framework that finds unused media using Special:Unusedimages. It places
a template (`:it:Template:Immagine
orfana <:it:Template:Immagine orfana>`__) on the image, and notifies the
user with a template (`:it:Utente:Filbot/Immagine
orfana <:it:Utente:Filbot/Immagine orfana>`__).

When run on an English project, it uses templates "No-use2" and
"img-sem-uso", but these are not known to exist anywhere. On English
Wikipedia there isnt any appropriate template, as `w:Template:Orphan
image <w:Template:Orphan image>`__ is strictly for use by free media,
and w:Template:orfud is used for fair use media.

Special:Unusedimages is known to not correctly skip media used by
mw:Extension:ProofreadPage, making it unsuitable for automated use on
Wikisource projects.

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/unusedfiles.py}}

`unusedfiles.py <Category:Pywikibot scripts>`__
