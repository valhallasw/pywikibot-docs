.. raw:: mediawiki

   {{MoveToMediaWiki}}

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/wikipedia.py}}

.. raw:: mediawiki

   {{svn/pywikipedia}}

.. raw:: mediawiki

   {{Pywikibot|script}}

.. raw:: mediawiki

   {{Cleanup}}

**wikipedia.py**\ (`1 <http://svn.wikimedia.org/svnroot/pywikipedia/trunk/pywikipedia/wikipedia.py>`__)
is a module available with the `pywikipedia
framework <Using the python wikipediabot>`__. Despite its name, it can
be used not only for Wikipedia, but for all other MediaWiki projects.
This module offers some classes and functions to be used in other
scripts. Running wikipedia.py itself directly, one would get the version
information as output.

Page class, site class and wikipedia.stopme() function
------------------------------------------------------

The most important class (and the most used) is the Page class. It
provides all the common action for a wikipage. To use that, you must
first of all call it, and only afterwards can you use its internal
function.

.. code:: python

    import wikipedia # Import the wikipedia module

    site = wikipedia.getSite() # Taking the default site
    page = wikipedia.Page(site, 'PAGENAME') # Calling the constructor
    print page
    wikipedia.stopme()

In the example, you import the wikipedia module. After that it's needed
to define the site where the page is. If you take it how it's done in
the example, you'll take the page that is in the project set in
user-config.py.

If you want to load the page of a different project you have to do as in
the following example. At the end, there is ``wikipedia.stopme()`` that
is needed so that your other bot processes aren't slowed down.

.. code:: python

    import wikipedia
    enWikisrcSite = wikipedia.getSite('en', 'wikisource') # loading a defined project's page
    page = wikipedia.Page(enWikisrcSite, 'Main Page')
    text = page.get() # Taking the text of the page
    print text
    wikipedia.stopme()

Rewrite code better
-------------------

In the previous example, you import wikipedia. The site is defined as
English Wikisource, with the parameters 'en' and 'wikisource'. Then we
define the Main Page as the page to take. And we load the text.

Then we print the text to the screen to let the user read it. Actually,
this code is not really clean and good. An experienced coder can improve
it as follows.

.. code:: python

    import wikipedia
    # Define the main function
    def main():
        titleOfPageToLoad = u'Main Page' # The "u" before the title means Unicode, important for special characters
        wikipedia.output(u'Loading %s...' % titleOfPageToLoad)
        enwiktsite = wikipedia.getSite('en', 'wikisource') # loading a defined project's page
        page = wikipedia.Page(enwiktsite, titleOfPageToLoad)
        text = page.get() # Taking the text of the page
        wikipedia.output(text) # Print the text, encoding it with wikipedia's method

    if __name__ == '__main__':
        try:
            main()
        finally:
            wikipedia.stopme()

This code is better than before for many reasons. First of all, it uses
a function and it's not procedural as before. In this way, the main
function will only be invoked if the script is called directly. This
makes it possible to import it from another script, making the code more
modular and reusable.

Furthermore, the try/finally block guarantees that stopme() is always
called, even when an exception is raised. This prevents the slowing down
of other process and is quicker when you test a script.

Another interesting new thing is the use of wikipedia.output(). It does
the same job of printing "something" but, and this is the important
thing, it encodes and decodes the text using the encoding defined in
user-config. This makes sure that special characters like Umlauts or
Cyrillic letters are shown correctly. **Note:** If you don't put the
text in the u"something" (with the u) the function will return a
(handled, but ugly to see) error. (the text variable contain already the
code encode in a good way, so it won't raise an exception).

Unfortunately, you can't always be sure that the page you are trying to
load exists. To prevent that, wikipedia.py will raise a NoPage
exception. You can use an except block to solve the problem, as in the
following example.

site.allpages() function and the wikipedia.py errors
----------------------------------------------------

.. code:: python

    import wikipedia
    # Define the main function
    def main():
        site = wikipedia.getSite()
        startpage = '!'
        for page in site.allpages(startpage): # Use a generator object, this will yield all pages one by one
            pagename = page.title() # Take the title of the page (not "[[page]]" but "page")
            wikipedia.output(u"Loading %s..." % pagename) # Please, see the "u" before the text
            try:
                text = page.get() # Taking the text of the page
            except wikipedia.NoPage: # First except, prevent empty pages
                text = ''
            except wikipedia.IsRedirectPage: # second except, prevent redirect
                wikipedia.output(u'%s is a redirect!' % pagename)
                continue
            except wikipedia.Error: # third exception, take the problem and print
                wikipedia.output(u"Some error, skipping..")
                continue     
            wikipedia.output(text) # Print the output, encoding it with wikipedia's method

    if __name__ == '__main__':
        try:
            main()
        finally:
            wikipedia.stopme()

Here, we can see our first generator object that is in wikipedia.py.
First of all, we define the site (it's suggested to do it immediately,
because it's quite impossible not to use a site's function if you need
to work with wikipedia). The second variable is the page from which the
Bot will load all the pages on your wikimedia's project.

Then, in the line below, you start a for cycle parsing every page on
Wikipedia. Look out, because the function allpages() isn't a
sub-function of wikipedia, but of site! (so, you can determine from what
project you want to load all the pages).

The allpages() function has optional parameter, one of these are the
start page (default = '!'), then there is the namespace (default = 0),
then if you want to include redirects (default: True), and the throttle
(default: True). In the example, if you wanted to use the optional
parameters as well, you would have used:

::

    def allpages(self, start = '!', namespace = 0, includeredirects = True, throttle = True)

In the line below, we load the page's title, in this way you don't print
[[Page]] but Page, so it's a better output. Two lines below, you find
the try/except block.

The Bot tries to load the page and if it doesn't exists (maybe someone
has deleted it while the bot was running) it will print only a empty
text (you can do what you want, I've choosen this only for explanation
purpose). If the page is a redirect, it will notify it and, to make sure
that nothing will happend, we put an extreme Exception that don't block
the Bot (for example, if there is a Spamfilter's problem, it will be
handled in this way). The possible Wikipedia's Errors are:

::

    *wikipedia.Error                General Error
    *wikipedia.NoUsername           the Username is not in user-config.py
    *wikipedia.NoPage               The Page does not exist
    *wikipedia.IsRedirectPage       The Page is a redirect page
    *wikipedia.IsNotRedirectPage    The Page is not a redirect page
    *wikipedia.LockedPage           The Page is locked
    *wikipedia.LockedNoPage         Page does not exist, and creating it is not possible because of a lock (cascading protection)
    *wikipedia.NoSuchEntity         No entity exist for this character
    *wikipedia.SectionError         The section specified by # does not exist
    *wikipedia.PageNotSaved         Saving the page has failed (General Error)
    *wikipedia.EditConflict         There has been an edit conflict while uploading the page
    *wikipedia.SpamfilterError      Saving the page has failed because the MediaWiki spam filter detected a blacklisted URL.
    *wikipedia.ServerError          Got unexpected server response
    *wikipedia.UserBlocked          Your username or IP has been blocked
    *wikipedia.PageNotFound         Page not found in list

wikipedia.Page(site, pagename).get() and wikipedia.Page(site, pagename).put() analysis
--------------------------------------------------------------------------------------

Now we have only done a few tests, but the real job of a Bot, on
Wikipedia, is to modify pages! It's not made to print in a DOS screen
what is in a page. So, let's try to make the Bot to put the text inside
a page.

Remark: the following code will send an error if the page doesn't exist,
to test this condition please use page.exists().

.. code:: python

    import wikipedia
    # Define the main function
    def main():
        site = wikipedia.getSite()
        pagename = 'Wikipedia:Sandbox'
        page = wikipedia.Page(site, pagename)
        wikipedia.output(u"Loading %s..." % pagename) # Please, see the "u" before the text
        try:
            text = page.get(force = False, get_redirect=False, throttle = True, sysop = False, 
                                                 change_edit_time = True) # text = page.get() <-- is the same
        except wikipedia.NoPage: # First except, prevent empty pages
            text = ''
        except wikipedia.IsRedirectPage: # second except, prevent redirect
            wikipedia.output(u'%s is a redirect!' % pagename)
            exit()# wikipedia.stopme() is in the finally, we don't need to use it twice, exit() will only close the script
        except wikipedia.Error: # third exception, take the problem and print
            wikipedia.output(u"Some Error, skipping..")
            exit()
        newtext = text + '\nThis is a nice test, deleteme please'
        page.put(newtext, comment='Bot: Test', watchArticle = None, minorEdit = True)  # page.put(newtext, 'Bot: Test') <-- is the same

    if __name__ == '__main__':
        try:
            main()
        finally:
            wikipedia.stopme()

In this script there are options specified that are already set by
default. This is to show examples of options that can be used with this
useful function. So, you can use ``text = page.get()`` to load the text
and only ``page.put(newtext, 'Bot: Test')`` to put the changes, if you
don't need to change the other options.

wikipedia.Page(site, pagename).get()
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  force = False : if force is set as True, the Bot will ignore all the
   exceptions raised, included redirects, so you won't get errors (but
   your code can make mistakes..)
-  get\_redirect = False : if it is set to True, the Bot won't stop
   itself but it will follow the redirect (f.e. if you have [[Php]] that
   redirects to [[PHP]], the bot will load PHP).
-  throttle = True : to slow down the Bot so as not to over-stress the
   Server. Within wikimedia projects, you must to set it to be True.

-  sysop = False: To get the page as sysop (you can log-in as sysop if
   you need to edit protected pages or to do something that only sysops
   can do).
-  nofollow\_redirects=False : Like force it won't raise an exception if
   you load a redirect... but it will raise in all the other cases.
-  change\_version\_date = True : set it to False if you have already
   loaded the page before and do not check this version for changes
   before saving.

wikipedia.Page(site, pagename).put()
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.put(newtext, comment='Bot: Test', watchArticle = None, minorEdit =
True)

-  newtext is the text that you'll put on Wikipedia
-  comment = None : is the comment that the Bot will use when it will
   make a change. (default = "Wikipedia python library")
-  watchArticle = None : if you want to put the article edited to your
   bot's watchlist you have to change it to True
-  minorEdit = True : The Bot will make a minor-edit. If it's not
   necessary, set it to True also if you make big-changes. **Note**: If
   you edit a user's talk page, if you want to let them know of the
   change that you've done, set this parameter to False otherwise set it
   to True.

If you want to change the default comment, you can use the function
wikipedia.setAction(text) to use text instead of "Wikipedia python
library" to be sure that your code won't have strange summary's
messages.

wikipedia.Page(site, pagename).getReferences(), .move(), .protect(), .delete() and .undelete()
----------------------------------------------------------------------------------------------

The Page class has a lot of function that let you make what you want and
there are so many function that also what you think that was impossibile
to do with a Bot can become reality. For example, do you know that (if
you are a sysop) you can load a deleted revision, using the Bot? (and
you can also undelete it!) But now it's better to explain the main and
most used function (by the way, you can find what you need also taking a
look at the code and searching ``def getDeletedRevision(``)

wikipedia.Page(site, pagename).getReferences()
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: python

    import wikipedia
    def main():
        page = wikipedia.Page(wikipedia.getSite(), 'Wikipedia:Sandbox')
        for pagetoparse in page.getReferences(follow_redirects=True, withTemplateInclusion=True, onlyTemplateInclusion=False, redirectsOnly=False):
            wikipedia.output(pagetoparse.title())
    if __name__ == '__main__':
        try:
            main()
        finally:
            wikipedia.stopme()

It's a generator, this means that it returns all the pages that
reference to the page defined with the wikipedia.Page() class. If you
need to load the entire list of referred pages to work with them, use:

::

    pages = [page for page in s.getReferences()]

Like the previous examples, you can use the reference function as:

.. code:: python

    for i in page.getReferences():
        wikipedia.output(i.title())

The parameters available are: (follow\_redirects=True,
withTemplateInclusion=True, onlyTemplateInclusion=False,
redirectsOnly=False):

-  follow\_redirect=True : as above, it returns also redirects if it's
   True (otherwise it won't return the redirects)
-  withTemplateInclusion=True : if you use a page as template, in the
   references appears a "included in page [...]" so, if you need only to
   load the pages that links to the page, set to True otherwise set to
   False.
-  onlyTemplateInclusion=False : if True, it will load only the pages
   that use the page as a Template and not the other.
-  redirectsOnly=False : if True, it will return only the redirects to
   the page

--- *Work in Progress* ---

See also
--------

-  `Using the python wikipediabot <Using the python wikipediabot>`__

`wikipedia.py <Category:Pywikibot scripts>`__
