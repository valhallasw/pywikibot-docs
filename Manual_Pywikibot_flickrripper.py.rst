**Flickrripper** is a `free <w:Free Software>`__ `Python <w:Python>`__
program for easy upload of large numbers of images from
`Flickr <:w:Flickr>`__ to Wikimedia Commons. The program is part of
`Pywikipedia <:m:Pywikipedia>`__ and is currently in pre-alpha state.
The tool was requested by some on `Commons:Batch uploading/Flickr images
by user <:Commons:Commons:Batch uploading/Flickr images by user>`__.

Installation
------------

Pywikipedia

Flickrripper is part of Pywikipedia. You first need to install
pywikipedia. At `Using the python
wikipediabot <Pywikipediabot/Basic use>`__ you can find a manual on how
to install pywikipedia. SVN install is recommended.

Easy install
~~~~~~~~~~~~

Easy install

We need to install 2 more packages. For this we need setuptools. You can
download the latest version at http://pypi.python.org/pypi/setuptools

Python Image Library

Python Image Library (PIL) is used to show the image. You can install it
by running the command at a command prompt:

    ``easy_install PIL``

Flickrapi kit

The `Python Flickrapi kit <http://stuvel.eu/projects/flickrapi>`__ is
used to communicate with the `Flickr
api <http://www.flickr.com/services/api/>`__. You can install it by
running the command at a command prompt:

    ``easy_install flickrapi``

TkInter
    You can install this library
    `1 <https://wiki.python.org/moin/TkInter>`__ with your usual package
    manager; don't forget the ``python-imaging-tk`` package.

pip
~~~

All of the above
    You should be able to install all of the above in one go, whatever
    permissions you have, with:
    ``pip install --user flickrapi pillow``

Flickr authentication
~~~~~~~~~~~~~~~~~~~~~

Flickr API key

You need a valid Flickr API key to run this program. You can apply for a
key `here <http://www.flickr.com/services/api/keys/apply/>`__. Apply for
a Non-Commercial API Key.

Configuration

If you recently installed pywikipedia your user-config.py contains a
flickr section, otherwise you have to add it to user-config.py yourself.
Edit user-config.py with your favorite text editor.

::

    # Using the Flickr api
    flickr = {
        'api_key': 'YOUR_API_KEY',  # Provide your key!
        'api_secret': 'YOUR_API_SECRET', # Provide your secret!
        'review': False,  # Do we use automatically make our uploads reviewed? (True or False)
        'reviewer': 'REVIEWER_NAME', # If so, under what reviewer name?
        }

-  api\_key : Provide your Flickr API key.
-  review : If you want to mark all images as review automatically. Use
   "True" only if you have a
   `reviewer <commons:Commons:License review>`__ or sysop flag on
   Commons!
-  reviewer : Add your username here if you want to mark images as
   reviewed by you.

Now you'll be requested to login on your first run of the script, to
confirm the application. The text login doesn't work (needs JavaScript),
it's better if you just run ``flickrripper.py`` on your home computer so
that the confirmation form is opened in your standard browser.

Usage
-----

To run Flickrripper you have to browse to the Pywikipedia folder. Then
type the following:

    ``python flickrripper.py``

with some of the various following options; the *necessary* ones are
bolded.

Notes:

-  the script never uploads duplicate files (identified with their
   hash);
-  unless the files you're uploading all have title, description etc.,
   edit the script to add a "prefix" to the filenames: look for the
   **``getFilename``** line, replace "Flickr" with your filename prefix
   in ``project=u'Flickr'`` (can be e.g. the name of the category you're
   using).

Options to tell what images to work on:

-  One of the following:

   #. -**group\_id** - The id of the Flickr group to work on. Works on
      all images in a group.
   #. -**photoset\_id** - The id of the Flickr set to work on. Works on
      all images in a set.
   #. -**user\_id** - The id of the user to work. Works on all images
      uploaded by a user. Username is not an id! For example, id for
      user `The Library of
      Congress <http://www.flickr.com/people/library_of_congress/>`__ is
      8623220@N02 (you can find it
      `here <http://www.flickr.com/services/api/explore/?method=flickr.people.findByUsername>`__).

-  One or both of:

   #. -start\_id - Start at the photo with this id (useful for resuming
      uploads). Use this in combination with
      -group\_id/-photoset\_id/-user\_id.
   #. -end\_id - Stop at the photo with this id (useful if you just want
      to do a part of the upload and later resume with -start\_id).

Options to tell how to work on each image:

#. -tags - Filter out a certain tag (only one at the moment, will be
   changed to support multiple tags).
#. -flickrreview - Mark as flickrreviewed, this overrides the settings
   in your user-config.py.
#. -reviewer - Set the reviewer for flickrreview, this overrides the
   settings in your user-config.py.
#. -override - Remove the licensing part and replace it with something
   custom. Can be used for transfering copyrighted photo's for which you
   have OTRS permission. Use with care!
#. -removecategories - Don't add categories from automatic suggestions.
#. -**addcategory** - Manually add a category, which you will be asked
   for after launching and will not be shown in the description in the
   confirmation dialog. Does not yet support multiple categories, but
   you can pass multiple as if they were one only, like this:
   ``FirstCategory]][[Category:SecondCategory``.
#. -autonomous - For autonomous uploading without showing of each image.
   Use with care!

Syntax:

    ``python flickrripper.py -user_id:8623220@N02 -removecategories -addcategory``

Troubleshooting
---------------

::

    Traceback (most recent call last):
      File "flickrripper.py", line 41, in <module>
        from PIL import Image, ImageTk    # see: http://www.pythonware.com/products/pil/
    ImportError: No module named PIL

You can fix this by `manual PIL
installation <http://www.pythonware.com/products/pil/>`__ (not by
easy\_install): «\ `If you’re using a prebuilt version of PIL, you might
need to install additional packages to be able to use the ImageTk
module. For example, on Ubuntu, you need both python-imaging and
python-imaging-tk <http://effbot.org/imagingbook/imagetk.htm>`__\ ».

`flickrripper.py <Category:Pywikibot scripts>`__
