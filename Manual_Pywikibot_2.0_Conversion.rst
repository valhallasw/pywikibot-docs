.. raw:: mediawiki

   {{outdated}}

This is a guide to converting from version 1 of the Pywikipediabot
framework to version 2.

Most importantly, note that the version 2 framework *only* supports
wikis using MediaWiki v.1.14 or higher software. If you need to access a
wiki that uses older software, you should continue using version 1 for
this purpose.

Installation
------------

The rewrite branch can be installed from the GIT server at
`gerrit.wikimedia.org <https://gerrit.wikimedia.org/r/#/admin/projects/pywikibot/core>`__,
or from the nightly snapshots available at
http://toolserver.org/~valhallasw/pywiki/

Make sure that the root of the rewrite package (the files you just
installed in the previous step) and the "pywikibot" directory in that
package are both in your
`PYTHONPATH <http://docs.python.org/using/cmdline.html#envvar-PYTHONPATH>`__
environment value, and that the "scripts" directory is in your PATH if
you want to run scripts from any working directory.

Python libraries
~~~~~~~~~~~~~~~~

The rewrite branch requires Python 2.5 or 2.6.

[Note: the goal will be to package pywikibot with setuptools
easy\_install, so that these dependencies will be loaded automatically
when the package is installed, and users won't need to worry about
this...]

You will also need the httplib2, simplejson, and setuptools packages--

-  httplib2 : http://code.google.com/p/httplib2/
-  setuptools : http://pypi.python.org/pypi/setuptools/
-  simplejson :
   http://svn.red-bean.com/bob/simplejson/tags/simplejson-1.7.1/docs/index.html

or, if you already have setuptools installed, just execute
'easy\_install httplib2' and 'easy\_install simplejson' [Note that
simplejson is only required for Python 2.5 users, since the equivalent
capability is built-in to 2.6.]

If you run into errors involving httplib2.urlnorm, update httplib2 to
0.4.0 (Ubuntu package python-httlib2, for example, is outdated). Note
that httplib2 will run under Python 2.6, but will emit
DeprecationWarnings (which are annoying but don't affect the ability to
use the package).

User files
~~~~~~~~~~

In most cases, an existing user-config.py that is being used with the
old framework should work unchanged with the rewrite branch. You will
need to copy that file into a user directory. To use the default path,
try to run "python config2.py" in the directory in which you installed
the package; you will get an error message that looks something like
"RuntimeError: No user-config.py found in directory 'C:\\Documents and
Settings\\username\\Application Data\\pywikibot'." (The default
directory name is different on non-Windows systems.) Just put your
user-config.py in the directory given by that message. If you don't like
the default, the specific path to the user directory can be changed by
setting the environment variable PYWIKIBOT2\_DIR in your shell. You can
also copy existing 'passwords' and 'user-fixes.py' files, if you have
them, to this directory.

Converting scripts
------------------

The root namespace used in the project has changed from "wikipedia" to
"pywikibot". References to wikipedia need to be changed globally to
pywikibot. Unless noted in this document, other names have not changed;
for example, wikipedia.Page can be replaced by pywikibot.Page throughout
any bot. An effort has been made to design the interface to be as
backwards- compatible as possible, so that in most cases it should be
possible to convert scripts to the new interface simply by changing
import statements and doing global search-and-replace on module names,
as discussed in this document.

With pywikipedia scripts were importing "wikipedia" or "pagegenerators"
libraries; pywikibot is now written as a standard package, and other
modules are contained within it (e.g., pywikibot.site contains Site
classes). However, most commonly-used names are imported into the
pywikibot namespace, so that module names don't need to be used unless
specified in the documentation.

The following changes, at a minimum, need to be made to allow scripts to
run:

| ``   change "import wikipedia" to "import pywikibot"``
| ``   change "import pagegenerators" to "from pywikibot import pagegenerators"``
| ``   change "import config" to "from pywikibot import config"``
| ``   change "import catlib" to "from pywikibot import catlib"``
| ``   change "wikipedia." to "pywikibot."``
| ``   change ".lang" to ".code" for site objects unless you want the language code and not the family code``

After converting, it is recommended to run your script in debug mode
(for example, ``python myscript.py -debug``) and review the (lengthy)
output in the log file (which will be found in the same user directory
that contains user-config.py, under the name myscript-bot.log) to see if
your script is using deprecated methods or giving other warning
messages.

Page objects
------------

The constructor syntax for Pages has been modified; existing calls in
the format of Page(site, title) will still work, and this is still the
preferred way of creating a Page object.

A second syntax allows creating a Page from a Link object (more on this
below), which handles link parsing and interpretation that doesn't
require access to the wiki server.

A third syntax allows easy conversion from a Page object to an ImagePage
or Category, or vice versa: for example, Category(pageobj) converts a
Page to a Category, as long as the page is in the category namespace.

The **site** attribute of Page objects has been changed from a method to
a property. This means that any code that uses ``p.site()`` on a Page
object ``p`` needs to be changed to use ``p.site`` instead.

Additionally, the **templatesWithParams()** method now returns a
generator that yields ``(page, parameters)`` tuples rather than
``(title, parameters)`` tuples.

The following methods of the Page object have been deprecated
(deprecated methods still work, but print a warning message in debug
mode):

urlname(): replaced by Page.title(asUrl=True)
titleWithoutNamespace(): replaced by Page.title(withNamespace=False)
sectionFreeTitle(): replaced by Page.title(withSection=False)
aslink(): replaced by Page.title(asLink=True)
encoding(): replaced by Page.site().encoding()

The following methods of the Page object have been obsoleted and no
longer work (but these methods don't appear to be used anywhere in the
code distributed with the bot framework). The functionality of the two
obsolete methods is easily replaced by using standard search-and-replace
techniques. If you call them, they will print a warning and do nothing
else:

-  removeImage()
-  replaceImage()

ImagePage objects
~~~~~~~~~~~~~~~~~

For ImagePage objects, the getFileMd5Sum() method is deprecated; it is
recommended to replace it with getFileSHA1Sum(), because MediaWiki now
stores the SHA1 hash of images.

Category objects
~~~~~~~~~~~~~~~~

The Category object has been moved from the catlib module to the
pywikibot namespace. Any references to "catlib.Category" can be replaced
by "pywikibot.Category", but the old form is retained for
backwards-compatibility.

For Category objects, the following methods are deprecated:

subcategoriesList: use, for example, list(self.subcategories()) instead
articlesList: use, for example, list(self.articles()) instead
supercategories: use self.categories() instead
supercategoriesList: use, for example, list(self.categories()) instead

``MORE TO COME``

`#2.0/Conversion <Category:Pywikibot>`__
