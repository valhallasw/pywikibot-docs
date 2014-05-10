.. raw:: mediawiki

   {{notice|Read access was implemented in [[pyrev:11182]].}}

A proposal on how the rewrite datapage/relevant classes should look:

.. code:: python

    #!/usr/bin/env python
    """
    Copyright (C) 2013 Pywikipediabot team
    Released under MIT License
    """
    import pywikibot
    from pywikibot.data import api

    class WikibasePage(Page):
        """
        The base page for the wikibase extension
        """
        def __init__(self, source, title=u""):
            pywikibot.Page.__init__(self, source, title)
            self._save = {'labels': {}, 'descriptions': {}, 'aliases': {}}  # holder

        def __get_language(self, source):
            if isinstance(source, pywikibot.Site):
                return source.language()
            source = source.replace('-','_')
            if not source.endswith('wiki'):
                source += 'wiki'
            return source

        def __normalize_qid(self, qid):
            try:
                int(qid)
                return 'q' + str(qid)
            except ValueError:
                if qid.lower().startswith('q'):
                    return qid.lower()
                    #at this point we just have bad input
            raise pywikibot.exceptions.BadTitle


        def __defined_by(self):
            """
            returns the parameters needed by the API
            to identify an item.
            Once an item's "q##" is looked up, that
            will be used for all future requests.
            """
            params = {}
            #qid overrides all
            if hasattr(self, 'id'):
                params['ids'] = self.id
                return params

            if not self.title().upper().startswith('P'):
                raise pywikibot.exceptions.BadTitle
            #the rest only applies to ItemPages, but is still useful here.

            if isinstance(self.site, pywikibot.Page):
                params['sites'] = self.__normalize_site(self.site.site())
                params['titles'] = self.site.title()
            elif isinstance(self.site, pywikibot.DataSite):
                params['ids'] = self.__normalize_qid(self.title)
            elif isinstance(self.site, pywikibot.Site):
                params['sites'] = self.__normalize_site(self.site)
                params['titles'] = self.title
            else:
                raise pywikibot.exceptions.BadTitle
            return params


        def get(self, force=False):
            """
            Fetches all page data, and caches it
            force will override caching
            """
            if force or not hasattr(self, '_content'):
                #action=wbgetentities&ids=Q42&format=jsonfm
                params = dict(**self.__defined_by())
                params['action'] = 'wbgetentities'
                req = api.Request(**params)
                data = req.submit()
                if not 'success' in data:
                    raise pywikibot.data.api.APIError, data['errors']
                self.qid = data['entities'].keys()[0]
                self._content = data['entities'][self.qid]
                #aliases
            self._aliases = {}
            for lang in self._content['aliases']:
                self._aliases[lang] = list()
                for value in self._content['aliases'][lang]:
                    self._aliases[lang].append(value['value'])
                    #labels
            self._labels = {}
            for lang in self._content['labels']:
                self._labels[lang] = self._content['labels'][lang]['value']

            #descriptions
            self._descriptions = {}
            for lang in self._content['descriptions']:
                self._descriptions[lang] = self._content['descriptions'][lang]['value']

            return {'aliases':self._aliases,
                    'labels':self._labels,
                    'descriptions':self._descriptions,
            }


        @property
        def label(self, lang=None):
            """
            Returns the label used by the specified language
            If no lang is specified, it returns a dict with all labels
            """
            if lang:
                return self.get()['labels'][self.__get_language(lang)]
            else:
                return self.get()['labels']

        @label.setter
        def label(self, text, lang):
            """
            Sets the label for the specified language
            """
            self._save['labels'][self.__get_language(lang)] = text

        @label.deleter
        def label(self, lang, summary=None):
            """
            Removes the label for the specified language (a site object0
            """
            self._save['labels'][self.__get_language(lang)] = None

        @property
        def description(self, lang=None):
            """
            Returns the description used by the specified language
            If no lang is specified, it returns a dict with all description
            """
            if lang:
                return self.get()['descriptions'][self.__get_language(lang)]
            else:
                return self.get()['descriptions']


        @description.setter
        def description(self, text, lang):
            """
            Sets the description for the specified language
            """
            self._save['descriptions'][self.__get_language(lang)] = text

        @description.deleter
        def description(self, lang):
            """
            Removes the description for the specified language
            """
            self._save['descriptions'][self.__get_language(lang)] = None

        @property
        def alias(self, lang=None):
            """
            Returns the alias used by the specified language
            If no lang is specified, it returns a dict with all aliases
            """
            if lang:
                return self.get()['descriptions'][self.__get_language(lang)]
            else:
                return self.get()['descriptions']


        @alias.setter
        def alias(self, text, lang, summary=None):
            """
            Sets the alias for the specified language
            """
            lang = self.__get_language(lang)
            if lang in self._save['aliases']:
                self._save['aliases'][lang].append(text)
            else:
                self._save['aliases'][lang] = list(text)


        @alias.deleter
        def alias(self, lang, summary=None):
            """
            Removes the alias for the specified language (a site object0
            """
            #TODO WRITEME
            pass

        def save(self, summary, **kwargs):
            """
            Save whatever we added/removed/etc.
            """
            #TODO WRITEME
            pass


    class ItemPage(WikibasePage):
        def __init__(self, source, title=u""):
            WikibasePage.__init__(self, source, title)
            if not self.title().upper().startswith(u'Q'):
                raise ValueError(u"'%s' is not a item page!" % title)

        def __init__(self, site, title=None):
            """
            defined by qid XOR site AND title
            options:
            site=pywikibot.Page & title=None
            site=pywikibot.DataSite & title=Q42
            site=pywikibot.Site & title=Main Page
            """
            self.site = site
            self.title = title
            if isinstance(self.site, pywikibot.Site):
                self.repo = self.site.data_repository()
            elif isinstance(self.site, pywikibot.Page):
                self.repo = self.site.site().data_repository()
            else:
                self.repo = self.site

        @staticmethod
        def itemByPage(cls, page):
            '''
            Get the ItemPage based on a Page that links to it
            '''
            return ItemPage(cls, page.site(), page.title())

        def __defined_by(self):
            """
            returns the parameters needed by the API
            to identify an item.
            Once an item's "q##" is looked up, that
            will be used for all future requests.
            """
            params = {}
            #qid overrides all
            if hasattr(self, 'id'):
                params['ids'] = self.id
                return params

            if isinstance(self.site, pywikibot.Page):
                params['sites'] = self.__normalize_site(self.site.site())
                params['titles'] = self.site.title()
            elif isinstance(self.site, pywikibot.DataSite):
                params['ids'] = self.__normalize_qid(self.title)
            elif isinstance(self.site, pywikibot.Site):
                params['sites'] = self.__normalize_site(self.site)
                params['titles'] = self.title
            else:
                raise pywikibot.exceptions.BadTitle
            return params

        def __normalize_site(self, siteobj):
            lang = siteobj.language()
            lang = lang.replace('-','_')
            lang += 'wiki'
            return lang

        def __make_site(self, dbname):
            lang = dbname.replace('wiki','')
            lang = lang.replace('_','-')
            return pywikibot.Site(lang, 'wikipedia')

        def __normalize_qid(self, qid):
            try:
                int(qid)
                return 'q' + str(qid)
            except ValueError:
                if qid.lower().startswith('q'):
                    return qid.lower()
                #at this point we just have bad input
            raise pywikibot.exceptions.BadTitle

        def get(self, force=False, *args):
            """
            Fetches all page data, and caches it
            force will override caching
            args are the values of props
            """
            if force or not hasattr(self, '_content'):
                #action=wbgetentities&ids=Q42&format=jsonfm
                params = dict(**self.__defined_by())
                params['action'] = 'wbgetentities'
                if args:
                    params['props'] = '|'.join(args)
                req = api.Request(**params)
                data = req.submit()
                if not 'success' in data:
                    raise pywikibot.data.api.APIError, data['errors']
                self.id = data['entities'].keys()[0]
                self._content = data['entities'][self.qid]
                #aliases
            self._aliases = {}
            for lang in self._content['aliases']:
                self._aliases[lang] = list()
                for value in self._content['aliases'][lang]:
                    self._aliases[lang].append(value['value'])
                #labels
            self._labels = {}
            for lang in self._content['labels']:
                self._labels[lang] = self._content['labels'][lang]['value']

            #descriptions
            self._descriptions = {}
            for lang in self._content['descriptions']:
                self._descriptions[lang] = self._content['descriptions'][lang]['value']

            #claims
            self._claims = []

            #sitelinks
            self._sitelinks = {}
            for dbname in self._content['sitelinks']:
                site = self.__make_site(dbname)
                self._sitelinks[site] = pywikibot.Page(site, self._content['sitelinks'][dbname]['title'])

            return {'aliases': self._aliases,
                    'labels': self._labels,
                    'descriptions': self._descriptions,
                    'sitelinks': self._sitelinks,
                    'claims': self._claims
            }

        def properties(self, force=False):
            """
            Get the various properties for that item.
            force will override caching
            """
            pass

        def sitelinks(self, force=False):
            """
            Get all of the sitelinks
            force will override caching
            """
            return self.get(force=force)['sitelinks']

        def sitelink(self, site, force=False):
            """
            Returns a page object for the specific site
            site is a pywikibot.Site
            force will override caching
            If the item doesn't have that language, raise NoPage
            """
            sitelinks = self.get(force=force)['sitelinks']
            if not site in sitelinks:
                raise pywikibot.NoPage
            else:
                return sitelinks[site]

        def addSitelink(self, page, overwrite=False, summary=None):
            """
            Will add a sitelink pointing to the pywikipedia.Page object provided
            Will not overwrite unless overwrite is set to True
            Summary is an optional edit summary to be provided
            """
            pass

        def removeSitelink(self, site, summary=None):
            """
            Site is a site object representing the language to be removed
            Summary is an optional edit summary to be provided
            """
            pass


    class PropertyPage(WikibasePage):
        def __init__(self, source, title=u""):
            WikibasePage.__init__(self, source, title)
            if not self.title(withNamespace=False).upper().startswith(u'P'):
                raise ValueError(u"'%s' is not a property page!" % title)

        def get_type(self):
            """
            Returns the type that this item uses
            Examples: item, commons media file, StringValue, NumericalValue
            """
            pass

    class QueryPage(WikibasePage):
        """
        For future usage, not implemented yet
        """
        raise NotImplementedError

    class Claim(PropertyPage):
        def __init__(self, site, pid, snak):
            """
            Defined by the "snak" value, supplemented by site + pid
            """
            PropertyPage.__init__(self, site, pid)
            pass

        def get_target(self):
            """
            Returns object that the property is associated with.
            """
            pass

        def get_sources(self):
            """
            Yields a PropertyInstance for each source
            """
            pass

        def add_source(self, source):
            """
            source is a PropertyInstance.
            adds it as a reference.
            """
            pass

