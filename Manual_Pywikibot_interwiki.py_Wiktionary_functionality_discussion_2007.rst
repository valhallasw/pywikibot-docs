.. raw:: mediawiki

   {{MoveToMediaWiki}}

.. raw:: mediawiki

   {{shortcut|WM:IW-WIKT}}

How should the Interwiki Bot work across Wiktionary projects?
-------------------------------------------------------------

This space has been set up so that folks from the various Wiktionary
projects can discuss their vision for the behavior of the Interwiki Bot
(currently known as RobotGMwikt). This was the result of a discussion on
the #wiktionary channel between GerardM, Connel MacKenzie, DmcDevit,
hippietrail, and ArielGlenn.

This is primarily a policy dicussion and only secondarily a technical
dicussion.

Tentative topics of discussion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Background/overview

       Since January 2005, wikt:User:RobotGMwikt has been providing
       Wiktionaries with his interwiki bot's services. Having a single
       person coordinate interwiki activities across all language
       Wiktionaries has provided considerable efficiency. To date, the
       bot has been running with the flags set to match on exact
       spelling only, and set to treat redirects as invalid pages.
       Editors of some of the independent language Wiktionaries have
       expressed concerns with these choices for the bot's behavior . It
       is our hope that this discussion will provide an avenue of
       discussion so that concerns about functionality can be heard,
       voted on, and addressed to everyone's mutual satisfaction.

#. Translation concerns (for this individual discussion)

       It is hoped that the meta Tower of Babel will be able to assist
       translating this page.

#. Notification concerns (for this individual discussion)

       All Wiktionaries are partisan to their language's concerns. No
       single Wiktionary should be forcing others to accept certain
       functionalities that are technologically avoidable and
       inappropriate for a particular language. We hope to get
       representative participation from at least the top 27
       Wikitionaries (those with over 10,000 valid entries) and at least
       partial representation from as many more of the smaller
       Wiktionaries. Accounts will be set up on each of the 143
       Wiktionaries in order to post a message linking to this page on
       their `wikt:Wiktionary:Beer
       parlour <wikt:Wiktionary:Beer parlour>`__ equivalent page.

           Notified: el, en, ja, ru, pl, ko
           Not yet notified:
           (`list <Wiktionary#List_of_Wiktionaries>`__) zh, fr, io, tr,
           vi, bg, nl, et, fi, gl, de, hu, is, id, it, ku, fa, pt, sr,
           es, sv, plus all smaller Wiktionaries.

#. How RobotGMwikt currently operates

       The `Pywikipediabot <Pywikipediabot>`__'s `interwiki.py <../>`__
       python program/script is used to link pages that have the exact
       same title on different language Wiktionaries. Currently it has
       the "Wiktionary" flag which does non-Wikipedia functions, in
       particular, forces the "-noredirects" behavior. For some
       languages this is appropriate, for others, it is considered to be
       unacceptable. Part of the outcome of this discussion is to
       provide an arena for languages to request the behavior they
       desire in a central location. Currently, the perception exists
       that the interwiki bot cannot "follow" redirects on some
       languages without breaking the perceived consistency (of
       interwiki links) on nl.wiktionary.org. If the nl.wikt: community
       confirms this behavior is desired and is perceived as correct
       (for the Dutch language) then every effort will be made to modify
       the interwiki bot code to prevent "incorrect" reflexive links on
       nl.wiktionary.org (and perhaps any other languages with the same
       concern) when providing other languages the ability to recognize
       redirect pages as valid interwiki link targets.

#. Problems with or limits of current operation
#. Short-term feature requests (broken down by language for per-language
   requirements)
#. Technical and logistical considerations
#. Specific detailed scenarios and explanations
#. Other versions of this bot currently running

       `w:ru:Участник:VolkovBot <w:ru:Участник:VolkovBot>`__ has been
       running on a number of wikts since May 2007. It apparently
       emulates the current behavior of RobotGMwikt.

Operational goals
~~~~~~~~~~~~~~~~~

        *Technical note: Do not use pipe-syntax link hiding anywhere in
        this discussion. Use **en:wikt:dog#English** for clarity, never
        \ `dog <en:wikt:dog#English>`__\ .*

#. What do all Wiktionaries *want* as a result of allowing interwiki
   links
   :;Simple example

           On en.wikt, there are entries for both en:wikt:dog#English
           and en:wikt:chien#French. The *lemmas* on the 'dog' page
           should point to corresponding *lemmas* on the
           fr:wikt:dog#Anglais page. The *lemmas* on the 'chien' page
           should point to corresponding *lemmas* on the
           `fr:wikt:chien#Français <fr:wikt:chien#Français>`__ page.
           Currently this is impossible. Instead, only the pages
           themselves (not the *lemmas*) are linked.

#. What Wiktionaries have other (language-specific) requirements

        **Polish Wiktionary** runs its own interwiki bot, which differs
        from the standard in two respects:
        1. It doesn't link to ru: (since ru: has over 82.000 empty
        templates, directing users there is a waste of their time);
        2. PL.wikt places interwiki "at top". The default settings of
        interwiki.py cause the script to add two empty lines at the top
        of all the pages it edits, which looks ugly. The interwiki.py
        script that runs on PL is modified in such a way that those
        extra lines are not added/are removed when encountered (the devs
        are notified of this bug).
        `tsca <user:tsca>`__ `[re <user talk:tsca>`__] 18:18, 2 August
        2007 (UTC)

            Thank you for your notes. I'm not sure #1 is precisely a
            *language* concern but is interesting. (Perhaps a reworded
            heading?) On en.wikt:, we allow those as it provides links
            to stubs that a human can then fill in. Personally, I agree
            that ru.wikt made a poor choice, allowing those stubs. But I
            don't see how preventing interwiki links to them is helpful.
            --`Connel MacKenzie <User:Connel MacKenzie>`__ 17:10, 3
            August 2007 (UTC)

#. What uses besides human navigation use interwiki links?
#. What technical concerns will arise from changing interwiki operation?

Goals of the discussion
~~~~~~~~~~~~~~~~~~~~~~~

#. Determine what changes, if any, would benefit the various Wiktionary
   projects (broken down per-language)
#. Rank desired changes by priority
#. Create a plan for implementation
#. (Possibly) move the bot to toolserver
#. (Possibly) find additional maintainers and administrators of the bot

Please check that these topics make sense, add descriptive paragraphs,
wikify... and generally turn this into a useful introduction. Thanks.

Other
=====

Redirects do have multiple functions
------------------------------------

The premise of automated functionality is that because things are equal
in a way that can be understood by a program functionality can be
automated. When you discuss giving redirects a function in interwiki
links, the first thing to realise is that redirects do not have a single
function.

Many redirects exist because of renames that have happened in the past.
The word that is redirected can be wrong in all languages (nederlands is
an example). These redirects should not be deleted; they have a function
that ensures that we provide a consistent service. You can ask Brion for
details.

There are redirects that point to "correct spelling". This is really
problematic; a word like color and colour are both correct, they have
different etymology and their pronunciation is quite distinct. Having
said this there are projects that use redirects from one to the other.
There is no obvious correct spelling so it is really arbitrary.

There are redirects that can not be made in this way because the
spelling is correct in "another" language.

There has been a lively discussion on IRC. I have been told that I
*have* to listen to the community. When the community does not show how
these problems can be overcome, I will stop running the interwiki bot.

A policy discussion that wishes to implement something that is
technically not feasible is not a discussion I care to participate in.
To me this is a waste of time.

Thanks, `GerardM <User:GerardM>`__ 07:13, 30 July 2007 (UTC)

    Right now there are not even any proposed features to implement, so
    it is a little soon to predict the outcome. In any case we need to
    understand the technical limitations of the bot (and MediaWiki
    platform) too; that is part of what this page is for.
    `ArielGlenn <User:ArielGlenn>`__ 08:51, 30 July 2007 (UTC)

        As I explained it is not a technical limitation, the issue is
        with the data itself. As redirects have multiple origins, it
        cannot be assumed that they have a single origin. What is the
        point of starting a discussion when all the features that have
        been discussed in the past are not feasible??
        `GerardM <User:GerardM>`__ 20:47, 30 July 2007 (UTC)

        It isn't a problem with the data though; it is a problem with
        people (human beings) navigating from one site to another. Do
        wikis sometimes have mistakes? Of course. But those are
        corrected as they are found. Bowing out of the discussion before
        it has begun is not very graceful. We haven't even begun to
        explore the possibilities of what the various Wiktionaries
        *want* as a result of having interwiki links. --`Connel
        MacKenzie <User:Connel MacKenzie>`__ 07:01, 2 August 2007 (UTC)

        Gerald: the way to solve a problem is to first figure out what
        we want, then (only then) what we can do, and then do it. If you
        begin with the limitations that you think you have, you'll never
        do anything new. (We couldn't go to the moon because no airplane
        flew high enough, so why think about it? Instead, we decided we
        wanted to go to the moon, and then figured out what we could do
        and got there ;-) A specific example: redirects on the en.wikt
        have essentially 3 origins: (1) page moves from errors, (2)
        intentionally created redirects for variant phrases and such,
        and (3) redirects left from the conversion script that moved
        everything to lower case. You say that makes the problem
        impossible. But *if we wanted to* we could easily separate them:
        created by move, created by edit, created by move and only edit
        was User:Conversion script. See? And please don't feel
        restricted by the limitations of *interwiki.py*, it is
        ill-suited to this task to begin with. `Robert
        Ullmann <User:Robert Ullmann>`__ 15:24, 25 September 2007 (UTC)

New prototype
-------------

The present *interwiki.py* run by RobotGMwikt and VolkovBot et al, works
by wandering about the wikis, looking for "translations": let's see,
w:en:Cat links to w:fr:Chat, and it links to w:it:Gatto (um, `w:it:Felis
sylvestris catus <w:it:Felis sylvestris catus>`__ ;-), so create a link
from en:Cat to it:Gatto and vice versa; This is horribly inefficient for
the wikts: we just need to know what article titles are there, we don't
need to look at the iwikis in the other entries. The load on the WMF
servers by runing the 'pedia version on the wikts must be immense, and
completely unneeded.

I've written a new program, being run on the en.wikt, that works
differently. It prescans a recent XML dump for the wikt it will be
updating. Then it reads Special:Allpages from the wikts, doing a 170-way
multi-way merge on the fly, retrieving new pages only as needed. Then
for each title in the local wikt, if the list of wikts doesn't match the
prescan, edit the page and update the iwikis.

It *only reads and writes the pages it is updating*.

Because it is only working on the "local" wikt, it is easy for a wikt to
use a modified policy; the pl.wikt can delete "ru" from the Exists set
after it is initialized, and do those separately, nl.wikt can modify the
allpages generator to skip titles wrapped with the "allpagesredirect"
CSS class, etc. (Although it is best to have them all working the same;
but what the "same" should be takes some working out, right?) `Robert
Ullmann <User:Robert Ullmann>`__ 15:24, 25 September 2007 (UTC)

    See en:wikt:User:Interwicket/code but understand that this is a
    trial version, it doesn't run on the standard pybot framework.
    `Robert Ullmann <User:Robert Ullmann>`__ 00:02, 26 September 2007
    (UTC)

`interwiki.py/Wiktionary functionality
discussion/2007 <Category:Pywikibot scripts>`__
