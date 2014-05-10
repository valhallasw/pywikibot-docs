**Picasa copier** is a `free <w:Free Software>`__ `Python <w:Python>`__
program for easy upload of large numbers of public images from `Picasa
(Google web albums) <:w:Picasa>`__ to Wikimedia Commons. The program is
part of `Pywikipedia <:m:Pywikipedia>`__ and is currently in
verification
state\ `1 <https://sourceforge.net/tracker/?func=detail&aid=3522917&group_id=93107&atid=603140>`__.

Installation
------------

Pywikipedia

Picasacopier is part of Pywikipedia. You first need to install
pywikipedia. At `Using the python
wikipediabot <Pywikipediabot/Basic use>`__ you can find a manual on how
to install pywikipedia. SVN install is recommended.

Easy install

We need to install 2 more packages. For this we need setuptools. You can
download the latest version at http://pypi.python.org/pypi/setuptools

Python Image Library

Python Image Library (PIL) is used to show the image. You can install it
by running the command at a command prompt:

    ``easy_install PIL``

Google Data API kit

The `Google data api
kit <https://code.google.com/p/gdata-python-client/>`__ is used to
communicate with the `Picasa web album
api <http://gdata-python-client.googlecode.com/hg/pydocs/gdata.html>`__.
(see `Installing Google Data API Python
Library <https://developers.google.com/gdata/articles/python_client_lib#library>`__)

Usage
-----

To run Picasacopier you have to browse to the Pywikipedia folder. Then
type the following:

    ``python picasacopier.py``

You are presented with various options:

    Options to tell what images to work on:

:#-user\_id - The id of the picasa web album user to work. Works on all
public images uploaded by a user. (e.g. if your email is
'test@gmail.com', your User ID is 'test')

:#-album\_id - The id of the Picasa web album. (look here `finding web
album id
number <http://groups.google.com/a/googleproductforums.com/d/msg/picasa/UkAx1-JhGOI/dkAeZ9FjLvMJ>`__)

    Options to tell how to work on each image:

    #. -picasareview - Mark as picasareviewed
    #. -reviewer - Set the reviewer for picasareview
    #. -override - Remove the licensing part and replace it with
       something custom. Can be used for transfering copyrighted photo's
       for which you have OTRS permission. Use with care!
    #. -removecategories - Remove the suggested categories
    #. -addcategory - Manually add a category (will be supporting
       multiple categories)
    #. -autonomous - For autonomous uploading without showing of each
       image. Use with care!

Syntax:

    ``python picasacopier.py -user_id:test -removecategories -addcategory:<category name>``

Troubleshooting
---------------

::

    Traceback (most recent call last):
      File "picasacopier.py", line 371, in <module>
        from PIL import Image, ImageTk    # see: http://www.pythonware.com/products/pil/
    ImportError: No module named PIL

You can fix this by `manually PIL
installation <http://www.pythonware.com/products/pil/>`__ (not by
easy\_install).

See also
--------

`Picasa Web Albums Data API Developer's
Guide <https://developers.google.com/picasa-web/docs/1.0/developers_guide_python>`__

`picasacopier.py <Category:Pywikibot scripts>`__
