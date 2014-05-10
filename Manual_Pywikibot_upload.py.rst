.. raw:: mediawiki

   {{MoveToMediaWiki}}

 **upload.py** is a `Pywikipediabot <Pywikipediabot>`__ script used to
upload images to a wiki.

Usage
-----

    python upload.py [Global-arguments] [-keep]
    [-filename:targetFilename] [-noverify] [URL-or-filename
    [description-text]]

Arguments
---------

+-------------+-------------------------------------------------------------------------+
| -keep       | Keep the filename as is                                                 |
+-------------+-------------------------------------------------------------------------+
| -filename   | Target filename                                                         |
+-------------+-------------------------------------------------------------------------+
| -noverify   | Do not ask for verification of the upload description if one is given   |
+-------------+-------------------------------------------------------------------------+

If any other arguments are given, the first is the URL or filename to
upload, and the rest is a proposed description to go with the upload. If
none of these are given, the user is asked for the file or URL to
upload. The bot will then upload the image to the wiki.

The script will ask for the location of an image, if not given as a
parameter, and for a description.

If the -filename argument is given, then it is used as the name of the
image on the wiki; otherwise it is based on the filename or url of the
input file.

If -keep is not specified, then the target filename undergoes some
further checking, and the user is asked for confirmation. The /
character is forbidden, and the filename extension (after the dot) must
be one of these: gif, jpg, jpeg, mid, midi, ogg, png, svg, xcf, djvu. If
the check is failed, then the user is prompted for a new filename.

Spaces in the filename will automatically be converted to underscores,
since mediawiki doesn't allow spaces. The encoding of the filename will
also be converted to the encoding used on the target site (typically
unicode). The script also attempts to convert the description to the
wiki's target encoding, or, as a last resort, will convert characters to
html entities.

Error detection is based on both the http status and the contents of the
response, which is assumed to be in English; error detection may fail if
the bot's account has been set not to show an English interface.

Output example
--------------

Example of output if no file name is given:

::

    C:\Users\t\Desktop\pywikipedia>upload.py
    No input filename given
    File or URL where image is now: C:\Users\t\Desktop\Dead7.jpg
    Reading file C:\Users\t\Desktop\Dead7.jpg
    The filename on the target wiki will default to: Dead7.jpg
    Enter a better name, or press enter to accept:
    The suggested description is:

    Do you want to change this description? ([y]es, [N]o) n
    Uploading file to dead:en via API....
    Upload successful.

    C:\Users\t\Desktop\pywikipedia>

.. raw:: mediawiki

   {{Manual:Pywikibot/Global_Options}}

See also
--------

-  Manual:Pywikibot/uploadmultiple.py
-  `commons:User:Nichalp/Upload
   script <commons:User:Nichalp/Upload script>`__

`upload.py <Category:Pywikibot scripts>`__
