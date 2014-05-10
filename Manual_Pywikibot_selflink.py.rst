 `selflink.py <category:Pywikibot scripts>`__ **selflink.py** is a
pywikipedia script which checks pages for self links, and then offers
the operator a chance to do something about those redundant links. For
instance, a self link to this page would be
``<nowiki>[[Manual:Pywikipediabot/selflink.py]]</nowiki>`` This
automatically emboldens the text, like
`{{FULLPAGENAME}} <{{FULLPAGENAME}}>`__, which is not usually desirable.

Syntax
------

The script is called by typing ``python selflink.py -''parameters''``
The parameters allowed are the same as those employed by
`pagegenerators.py <Manual:Pywikipediabot/pagegenerators.py>`__, giving
you a wide variety of ways to check your wiki for self links. Consult
that page for a complete list of possible parameters. Parameters are
necessary for the operation of this script. If you type just
``python selflink.py`` you will be given a dump of the help file
informing you of the fact that you need to add a parameter.

Usage
-----

Once the script starts searching through your pages, it will stop
whenever it finds a self link and give you the opportunity to either
leave it alone, change it to "proper" bold text, as in
``<nowiki>[[London]] --> '''London'''</nowiki>``. Or you can simply
unlink it, as with ``<nowiki>[[London]] --> London</nowiki>``.

You can also chose to "unlink all", but this is unadvisable. Some
editors actively choose to use a self link in the leads of articles,
since it has the same net effect as "proper" bolding. Thus, choosing to
"unlink all" would put the script on "automatic" and potentially deprive
some articles of bold text at the beginning of some articles. Since many
wikis require this in their manuals of style, running this bot on
automatic could do more harm than good.

Happily, unlike most other pywikipedia scripts, this one allows you to
choose what should be done with each self link *individually*. So if you
have three self links on a single page, it'll ask you what to do with
*each one*, rather than changing the whole page at once. This allows you
to embolden self links in the leads of articles, but unlink them in the
infobox or body of the article.
