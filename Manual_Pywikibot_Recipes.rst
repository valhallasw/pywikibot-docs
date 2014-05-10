.. raw:: mediawiki

   {{Template:Pywikipediabot}}

.. raw:: mediawiki

   {{Bothelp}}

On this page you will find short snippets of code showing the framework
usage by the various bots.

Get language links for all pages
--------------------------------

Iterate through wiki pages (possibly with additional filters), and for
each page get all listed languagelinks.

```query&generator=allpages&gapfrom=T&prop=langlinks`` <http://en.wikipedia.org/w/api.php?action=query&generator=allpages&gapfrom=T&prop=langlinks>`__

-  API langlinks limits could make result incomplete for any page
   without any notification, making batch processing much more difficult
   - client needs to do more querycontinue calls to know there are no
   more langlinks for the specific page.

    **Pywikipediabot**

.. code:: python

    # Please write the proper code snippet here

Get language links for a set of pages
-------------------------------------

For a user-supplied list of titles, resolve redirects and get their
language links.

```query&prop=langlinks&titles=T|TT&redirects`` <http://en.wikipedia.org/w/api.php?action=query&prop=langlinks&titles=Main%20Page&redirects>`__

    **Pywikipediabot**

.. code:: python

    # Please write the proper code snippet here

Get non-resolved links and categories for a set of redirected pages
-------------------------------------------------------------------

For each page in a set, if redirect, resolve to the redirect target, and
get all links and all categories listed. Only link's namespace+title is
needed.

```query&prop=links|categories&titles=Archiver|Abstract%20(law)&pllimit=300&redirects`` <http://en.wikipedia.org/w/api.php?action=query&prop=links|categories&titles=Archiver|Abstract%20(law)&pllimit=300&redirects>`__

    **Pywikipediabot**

.. code:: python

    # Please write the proper code snippet here

Page generator -> get links and categories
------------------------------------------

From all pages in a wiki (possibly filtered), get all links and all
categories listed. Only link's namespace+title is needed. Result pages
(not links) might need to be edited.

```query&generator=allpages&gapfrom=T&prop=links|categories`` <http://en.wikipedia.org/w/api.php?action=query&generator=allpages&gapfrom=T&prop=links|categories>`__

    **Pywikipediabot**

.. code:: python

    # Please write the proper code snippet here

Modify a page
-------------

Given a page title, get the page content (if redirect, get the target),
change and save it.

| ```query&titles=Think&redirects&prop=revisions&rvprop=content`` <http://en.wikipedia.org/w/api.php?action=query&titles=Think&redirects&prop=revisions&rvprop=content>`__
| ``[``\ ```http://en.wikipedia.org/w/api.php?action=edit&summary`` <http://en.wikipedia.org/w/api.php?action=edit&summary>`__\ ``=...&text=...&token=... edit&summary=...&text=...&token=...]``

    **Pywikipediabot**

.. code:: python

    # This sample does not resolve redirects. Need more feedback.
    page = Page(pywiki.getSite('en'), u'Think')
    oldcontent = page.get()
    summary, newcontent = modify_page_text(oldcontent)
    page.put(summary, newcontent)

