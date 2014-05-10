.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/imagetransfer.py}}

**Imagetransfer.py** is a `Pywikipediabot <Pywikipediabot>`__ script
that copies images from one wiki to another wiki. To transfer image to
Wikimedia Commons use
`imagecopy.py <Manual:Pywikipediabot/imagecopy.py>`__.

Usage
-----

::

    python imagetransfer.py [common-arguments] pagename [-interwiki] [-tolang:xx] [-tofamily:yy]

Arguments
---------

::

    -interwiki   Look for images in pages found through interwiki links.
    -keepname    Keep the filename and do not verify description while replacing
    -tolang:xx   Copy the image to the wiki in language xx
    -tofamily:yy Copy the image to a wiki in the family yy
    -file:zz     Upload many files from textfile: [[Image:xx]]
                                                  [[Image:yy]]

If pagename is an image description page, the script offers to copy the
image to the target site.

If pagename is a normal page, it will offer to copy any of the images
used on that page.

If -interwiki is used, any of the images used on a page are reachable
via interwiki links. (i.e. The interwiki link [[Food]] is found on the
page Cake. The bot will search both the food and the cake page for
images).

.. raw:: mediawiki

   {{:Manual:Pywikibot/Global Options}}

`imagetransfer.py <Category:Pywikibot scripts>`__
