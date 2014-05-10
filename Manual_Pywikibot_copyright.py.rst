 **Copyright.py** is a script of the `Pywikipedia
bot <Manual:Pywikipediabot/Basic use>`__ framework that checks copyright
text in Google, Yahoo! and Live Search.

Google search requires to install the pyGoogle module from
http://pygoogle.sf.net and get a Google API license key from
http://code.google.com/apis/soapsearch/ (but since December 2006 Google
is no longer issuing new SOAP API keys).

Yahoo! search requires pYsearch module from
http://pysearch.sourceforge.net (Debian and Ubuntu package this as
``python-pysearch`` or
``python-yahoo<tt>, depending on your version) and a Yahoo AppID from http://developer.yahoo.com. (For Wikimedia projects, a [[wikitech:Web search|Yahoo! BOSS]] key exists.)

Windows Live Search requires to install the SOAPpy module from http://pywebsvcs.sf.net (Debian and Ubuntu package this as <tt>python-soappy``)
and get an AppID from http://search.msn.com/developer.

Configuration
-------------

Before use the script you have to add to user-config.py one or more
search engine keys. For example:

.. code:: python

    yahoo_appid = 'Key'
    msn_appid = 'Key'

Parameters
----------

g
    Use Google search engine
ng
    Do not use Google
y
    Use Yahoo! search engine
ny
    Do not use Yahoo!
maxquery
    Stop after a specified number of queries for page (default: 25)
new
    Check only the new pages
repeat
output
    Use this option to enable the output
    Append results to a specified file (default: 'copyright/output.txt')
file
    Work on all pages given in a local text file. Will read any `wiki
    link <wiki link>`__ and use these articles. Argument can also be
    given as "-file:filename".
cat
    Work on all pages which are in a specific category. Argument can
    also be given as "-cat:categoryname".
subcat
    When the pages to work on have been chosen by -cat, pages in
    subcategories of the selected category are also included. When -cat
    has not been selected, this has no effect.
page
    Only check a specific page. Argument can also be given as
    "-page:pagetitle". You can give this parameter multiple times to
    check multiple pages.
ref
    Work on all pages that link to a certain page. Argument can also be
    given as "-ref:referredpagetitle".
filelinks
    Works on all pages that link to a certain image. Argument can also
    be given as "-filelinks:ImageName".
links
    Work on all pages that are linked to from a certain page. Argument
    can also be given as "-links:linkingpagetitle".
start
    Work on all pages in the wiki, starting at a given page.
namespace:n
    Number of namespace to process. The parameter can be used multiple
    times.

Examples
--------

If you want to check first 50 new articles then use this command:

``python copyright.py -new:50``

If you want to check a category with no limit for number of queries to
request, use this:

``python copyright.py -cat:"Wikipedia featured articles" -maxquery:0``

`copyright.py <Category:Pywikibot scripts>`__
