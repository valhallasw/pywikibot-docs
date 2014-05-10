**Panoramiopicker** is a `free <w:Free Software>`__
`Python <w:Python>`__ program for easy upload of large numbers of images
from `Panoramio <:w:Panoramio>`__ to Wikimedia Commons. The program is
part of `Pywikipedia <:m:Pywikipedia>`__ and is currently in pre-alpha
state.

Installation
------------

Pywikipedia

Panoramiopicker is part of Pywikipedia. You first need to install
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

Configuration

If you recently installed pywikipedia your user-config.py contains a
panoramio section, otherwise you have to add it to user-config.py
yourself. Edit user-config.py with your favorite text editor.

::

    # Configuration of panoramiopicker.py
    panoramio = {
        'review': False,  # Do we use automatically make our uploads reviewed? (True or False)
        'reviewer': 'REVIEWER_NAME', # If so, under what reviewer name?
        }

-  review : If you want to mark all images as review automatically. Use
   "True" only if you have a
   `reviewer <commons:Commons:License review>`__ or sysop flag on
   Commons!
-  reviewer : Add your username here if you want to mark images as
   reviewed by you.

Usage
-----

To run Panoramiopicker you have to browse to the Pywikipedia folder.
Then type the following:

    ``python panoramiopicker.py``

You are presented with various options:

    Options to tell what images to work on:

    #. set - The id of the Panoramio user to work on. Works on all
       images uploaded by a user. Username is not an id! For example, id
       for user `Alexxx1979 <http://www.panoramio.com/user/5528490/>`__
       is 5528490 (you can find it in URL).
    #. -start\_id - Start at the photo with this id (useful for resuming
       uploads). Use this in combination with -set
    #. -end\_id - Stop at the photo with this id (useful if you just
       want to do a part of the upload and later resume with -start\_id)

    Options to tell how to work on each image:

    #. -tags - Filter out a certain tag (only one at the moment, will be
       changed to support multiple tags).
    #. -panoramioreview - Mark as panoramioreviewed, this overrides the
       settings in your user-config.py
    #. -reviewer - Set the reviewer for panoramioreview, this overrides
       the settings in your user-config.py
    #. -override - Remove the licensing part and replace it with
       something custom. Can be used for transfering copyrighted photo's
       for which you have OTRS permission. Use with care!
    #. -addcategory - Manually add a category (will be changed to
       support multiple categories)
    #. -autonomous - For autonomous uploading without showing of each
       image. Use with care!

Syntax:

    ``python panoramiopicker.py -set:5528490 -addcategory``

Troubleshooting
---------------

::

    Traceback (most recent call last):
      File "panoramiopicker.py", line 28, in <module>
        from PIL import Image, ImageTk    # see: http://www.pythonware.com/products/pil/
    ImportError: No module named PIL

You can fix this by `manually PIL
installation <http://www.pythonware.com/products/pil/>`__ (not by
easy\_install).

`panoramiopicker.py <Category:Pywikibot scripts>`__
