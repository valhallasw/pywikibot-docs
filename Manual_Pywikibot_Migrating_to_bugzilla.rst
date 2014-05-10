Migration plan
^^^^^^^^^^^^^^

Note: SF.net has just migrated the project from the old bug tracker
system to the new one ('Allura'). See
https://sourceforge.net/p/pywikipediabot/bugs/

-  Tracking bug: bugzilla:52692

WMF Contacs
'''''''''''

-  André Klapper (User:AKlapper_(WMF)) can help us set up bugzilla

Name
''''

pywikipedia

-  Pywikipedia (per mailing list) or Pywikipediabot (per
   Manual:Pywikipediabot) are simple enough. `Legoktm <User:Legoktm>`__
   (`talk <User talk:Legoktm>`__) 21:34, 10 June 2013 (UTC)
-  I agree on pywikipedia because I think "bot" is redundant, see other
   py tools, numpy not numpytools, scipy not scipysimulationpackage :D,
   ... `Ladsgroup <User:Ladsgroup>`__ (`talk <User talk:Ladsgroup>`__)
   00:47, 12 June 2013 (UTC)
-  I propose **pywikibot** which is the group name in git/gerrit. The
   bot is not only for Wikipedia but for other wikis too.
    \ `@ <user talk:xqt>`__\ \ `xqt <user:xqt>`__ 16:39, 14 August 2013
   (UTC)

   -  Because we named git/gerrit pywikibot, I'm fine with naming it the
      same here. `Multichill <User:Multichill>`__
      (`talk <User talk:Multichill>`__) 10:46, 18 August 2013 (UTC)
   -  personally I prefer pywikipedia but because other people prefer
      pywikibot (and they used it in git, nightlies, pywikibot-commits-l
      and so many other places) so I support "pywikibot" because of
      homogeneity (unity) `Ladsgroup <User:Ladsgroup>`__
      (`talk <User talk:Ladsgroup>`__) 15:07, 18 August 2013 (UTC)

Components
''''''''''

The current sf.net labels are:

-  Category
-  copyright
-  cosmetic\_changes
-  Genral
-  GUI
-  i18n
-  interwiki
-  login
-  network
-  other
-  redirect
-  rewrite
-  solve\_disambiguation
-  weblinkchecker

-  I think we should use categories of sf as components
   `talk <User talk:Ladsgroup>`__) 03:54, 12 June 2013 (UTC)
-  I think we should change this, for example no more need of interwiki
   but we should add wikidata, and we should correct order of this list
   (It's totally alphabetical now) for example general must be first and
   other must be last\ `Ladsgroup <User:Ladsgroup>`__
   (`talk <User talk:Ladsgroup>`__) 00:47, 12 June 2013 (UTC)

   -  Bugzilla only allows components to be sorted by alphabet.
      --`AKlapper (WMF) <User:AKlapper (WMF)>`__
      (`talk <User talk:AKlapper (WMF)>`__) 07:55, 10 August 2013 (UTC)

      -  Components are good to make small area's of interest. We should
         have components for the different low level parts in core and
         compat, maybe for different libraries that are used by several
         tools and probably for the different (heavy usage) tools. We
         can always add/remove components if needed.
         `Multichill <User:Multichill>`__
         (`talk <User talk:Multichill>`__) 10:50, 18 August 2013 (UTC)

Amir's Proposal
               

-  category
-  copyright
-  cosmetic\_changes
-  Genral
-  i18n
-  login
-  network
-  redirect
-  solve\_disambiguation
-  weblinkchecker
-  wikidata

What do you think? `Ladsgroup <User:Ladsgroup>`__
(`talk <User talk:Ladsgroup>`__) 09:36, 15 August 2013 (UTC)

Linking bugs
''''''''''''

-  how can we make sure bugs link to eachother? i.e. a link from BZ to
   sf.net and from sf.net to BZ? - `Valhallasw <User:Valhallasw>`__
   (`talk <User talk:Valhallasw>`__) 20:36, 10 June 2013 (UTC)

   -  Tickets in Bugzilla have a "See Also" field which allows adding
      Sourceforge.net URLs. --`AKlapper (WMF) <User:AKlapper (WMF)>`__
      (`talk <User talk:AKlapper (WMF)>`__) 07:55, 10 August 2013 (UTC)

SF.net export
'''''''''''''

-  how can we get an export from sf.net? I know there \*should\* be a
   button, but I can't find it. If you need any sf.net permissions for
   this, let me know. - `Valhallasw <User:Valhallasw>`__
   (`talk <User talk:Valhallasw>`__) 20:36, 10 June 2013 (UTC)

Due to the upgrade, the old export function (which exports XML) will not
be updated. The current version does not have backup functionality (see
`this bug <https://sourceforge.net/p/allura/tickets/3154/>`__), but
there is a REST API:
`docs <https://sourceforge.net/p/forge/documentation/Allura%20API/#tracker>`__
`example
1 <https://sourceforge.net/rest/p/pywikipediabot/feature-requests>`__
`example
2 <https://sourceforge.net/rest/p/pywikipediabot/feature-requests/339>`__

Anonymous bugs
''''''''''''''

Can we allow anonymous/openid submitted bugs? I think there has been
discussion about this on wikitech-l, so it might be good to bump that. -
`Valhallasw <User:Valhallasw>`__ (`talk <User talk:Valhallasw>`__)
20:36, 10 June 2013 (UTC)

-  I strongly disagree about it but i think we should obey general
   bugzilla policies (If it will be changed)
   `talk <User talk:Ladsgroup>`__) 03:54, 12 June 2013 (UTC)

See these threads:
`1 <http://thread.gmane.org/gmane.science.linguistics.wikipedia.technical/68126/focus=70516>`__
`2 <http://thread.gmane.org/gmane.science.linguistics.wikipedia.technical/70520>`__
for OpenID progress.

-  

   -  Once OpenID is generally available in Wikimedia land we can start
      experimenting. Also see
      https://bugzilla.mozilla.org/show_bug.cgi?id=294608 and maybe
      https://github.com/jalcine/bugzilla-openid/blob/master/Extension.pm

Mailing list
''''''''''''

Pywikipedia-bugs should be switched. We probably need to add the
bugzilla mail address as permitted sender?

Does BZ support sending only pwb bugs to this mailing list?

    Yes, we can just add it as a default CC. `Legoktm <User:Legoktm>`__
    (`talk <User talk:Legoktm>`__) 15:58, 13 June 2013 (UTC)

        Updated
        `pywikipedia-bugs <https://lists.wikimedia.org/mailman/listinfo/pywikipedia-bugs>`__
        so that bugzilla can post to it.
        `Multichill <User:Multichill>`__
        (`talk <User talk:Multichill>`__) 10:54, 18 August 2013 (UTC)

Closed bugs
'''''''''''

-  we don't need to import closed bugs is there any objection about it?
   `Ladsgroup <User:Ladsgroup>`__ (`talk <User talk:Ladsgroup>`__)
   03:54, 12 June 2013 (UTC)
-  +1  \ `@ <user talk:xqt>`__\ \ `xqt <user:xqt>`__ 16:43, 14 August
   2013 (UTC)

Importing
---------

I've started putting together some code at
`3 <https://github.com/pywikibot/sf-export>`__ (requested a repo in
gerrit for it), to export from sf into bugzilla. Few questions:

-  Should all the history be in the first comment? Or should each
   comment be individual comments like in bugzilla:2?
-  Should we mark the sf.net bugs as closed? Or just leave a comment
   with the bugzilla link and keep them open forever.

Thanks, `Legoktm <User:Legoktm>`__ (`talk <User talk:Legoktm>`__) 05:01,
19 August 2013 (UTC)

    I think multiple comments is easier to understand. As for closing
    the bugs - maybe we can create a status 'Moved to bugzilla' on
    sf.net, which disables commenting? I have to check that for you.
    `Valhallasw <User:Valhallasw>`__ (`talk <User talk:Valhallasw>`__)
    08:17, 19 August 2013 (UTC)

    Example: I've filed
    http://sourceforge.net/p/pywikipediabot/patches/617/ some months
    ago: it could be closed on sf.net, because of gerrit:80698, but I
    still can't found a bugzilla equivalent.
    --\ `Ricordi <User:Ricordisamoa>`__\ `samoa <User talk:Ricordisamoa>`__\ 
    02:44, 3 September 2013 (UTC)

        I really don't get Sourceforge.net here. So there are bugs and
        enhancement requests. And there are "patches". To me, a bug or
        an enhancement request receive a patch to fix them. So "Patch"
        is just the "next step" after filing a bug or enhancement.
        --`AKlapper (WMF) <User:AKlapper (WMF)>`__
        (`talk <User talk:AKlapper (WMF)>`__) 08:15, 3 September 2013
        (UTC)

            This system belongs to the svn era not git so when someone
            make a patch and send a patch request, means someone with
            access has to merge the patch, we don't need this anymore
            `Ladsgroup <User:Ladsgroup>`__
            (`talk <User talk:Ladsgroup>`__) 14:33, 9 September 2013
            (UTC)

Script to-dos
-------------

-  OAuth login to sf.net - I have a patch for this locally
   `Legoktm <User:Legoktm>`__ (`talk <User talk:Legoktm>`__) 17:49, 2
   September 2013 (UTC)
-  Set priority based on where bug came from (bugs -> normal, feature
   requests -> enhancement)

       .. raw:: mediawiki

          {{done}}

       `Ladsgroup <User:Ladsgroup>`__ (`talk <User talk:Ladsgroup>`__)
       12:10, 20 September 2013 (UTC)


