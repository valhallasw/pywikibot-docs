.. raw:: mediawiki

   {{notice|1=
   <div style="text-align:center;">'''Dear Pywikipedia users!'''</div>
   Old versions of [[:en:Python (programming language)|Python]] cause several problems in maintenance of '''[[Manual:Pywikipediabot|Pywikipediabot]]'''. We look into the future and think that '''Python 2.7.2''' and newer is a good choice for Pywikibot as it has many features backported from Python 3.1, is free of an annoying Unicode bug involving versions up to 2.7.1, and may hope the [http://docs.python.org/whatsnew/2.7.html#the-future-for-python-2-x longest support time] from Python developers.

   The developer team would like to know how many people and for what reasons use still old Python versions from 2.4 to 2.7.1 in order to determine the support time of these versions. If you have to use versions listed below and really can't upgrade to 2.7.2 (or make your sysop upgrade), please share your circumstances with us here in the appropriate section. (Except WMDE Toolserver users – we know that toolserver uses 2.7.1.)

   Thank you for your attention!
   <div style="text-align:right;">''The Pywikipedia Developer Team''</div>}}

.. raw:: mediawiki

   {{mbox|type=warning|text=If you don't want to see the message that led you here on your screen any more, write the line<br>
   <tt>suppresssurvey = True</tt><br>
   into your <tt>user-config.py</tt>. This may be removed later when the survey is over.
   }}

Python 2.4 users
----------------

*Edit this section if you have a serious reason to use this version of
Python*

Python 2.5 users
----------------

*Edit this section if you have a serious reason to use this version of
Python*

ISO 8859-2
~~~~~~~~~~

I am using Windows XP CZ (SP2) (ISO 8859-2) on two different computers.

When I have in my user-config no ``console_encoding``:

Py 2.5 :

-  I have good czech characters in terminal window
-  I can write e.q. ``interwiki.py Dobříš``
-  I can write e.g. ``interwiki.py`` and after ask I write ``Dobříš``

Everything works well for me

Py 2.6+

-  I have bad czech characters in terminal window (ˇ instead of í, " "
   instead of á, nothing instead of ů, ý instead of ř....)
-  I can write e.g. ``interwiki.py Dobříš``
-  I can write e.g. ``interwiki.py and after ask I write Dobříš``

I am not able to read in terminal window

With ``console_encoding='windows-1250'``

Py 2.6+

-  I have good czech characters in terminal window
-  I can write e.q. ``interwiki.py Dobříš``
-  I can't write e.g. ``interwiki.py`` and after ask I write ``Dobříš``

I am not able to write to terminal window

With ``console_encoding='utf-8'``

Py 2.6+

-  I have bad non-base-ASCII characters in terminal window (two or three
   instead of one, translitertation for cyrilic or asian languages
   doesn't work
-  I can't write e.q. ``interwiki.py Dobříš`` - bot crashes
-  I can't write e.g. ``interwiki.py`` and after ask I write ``Dobříš``
   - bot crashes

I am not able to read or write to terminal window

With ``console_encoding='ISO 8859-2'``

-  I have good czech characters in terminal window
-  I can't write e.q. ``interwiki.py Dobříš`` - page does not exist
-  I can't write e.g. ``interwiki.py`` and after ask I write ``Dobříš``
   - page does not exist, bad chars in terminal window

I am not able to write to terminal window

`JAn Dudík <User:JAn Dudík>`__ (`talk <User talk:JAn Dudík>`__) 07:01,
13 March 2012 (UTC)

    I can confirm there has been a change in console output between
    python 2.5 and later versions. Instead of having codepage-dependant
    output, it seems windows-1252 is consistently used. However, all of
    this is caused by the crappy console in windows. However, I'm
    working on a solution that makes all code page crap irrelevant.
    `Valhallasw <User:Valhallasw>`__ (`talk <User talk:Valhallasw>`__)
    21:19, 25 March 2012 (UTC)

        On a side note, your codepage will not be 1250 but rather 852.
        Or something. I don't even know what the codepage does in what
        context anymore. `Valhallasw <User:Valhallasw>`__
        (`talk <User talk:Valhallasw>`__) 21:20, 25 March 2012 (UTC)

`Solved. <http://lists.wikimedia.org/pipermail/pywikipedia-l/2012-April/007495.html>`__
`Bináris <user:Bináris>`__\ :sup:``talk <user talk:Bináris>`__` 17:40,
16 April 2012 (UTC)

Running pywikipediabot on a pretty old but very stable Solaris server
where I don't have root access anymore. The software there does not
really get upgraded; I will try to prepare a non-root install of newer
python 2, but for now it's a nuisance.
 « `Saper <User:Saper>`__\  // `talk <User talk:Saper>`__\  »  08:43, 5
May 2012 (UTC)

    Fixed `a bug <Special:Code/pywikipedia/10918>`__ just introduced
    that broke 2.5...
     « `Saper <User:Saper>`__\  // `talk <User talk:Saper>`__\  » 
    11:00, 14 January 2013 (UTC)

Python 2.6 users
----------------

*Edit this section if you have a serious reason to use this version of
Python*

-  I use Cygwin and it seems, that Cygwin `don't
   support <http://cygwin.com/packages/python/>`__ 2.7. Of course it
   minor issue, because Cygwin using it's a perversion :-)
   --`Movses <User:Movses>`__ (`talk <User talk:Movses>`__) 21:55, 10
   March 2012 (UTC)
-  Cygwin and Debian 6.0 *squeeze* `Guaka <User:Guaka>`__
   (`talk <User talk:Guaka>`__) 19:28, 18 March 2012 (UTC)

   -  In Squeeze it's not so hard to fetch python 2.7.2 source, do
      ./configure; make; sudo make install and run scripts like
      /usr/local/bin/python2.7 but now it seems I might want to have the
      bot running from RHEL5 (with is 2.5 or 2.6 or so).
      `Guaka <User:Guaka>`__ (`talk <User talk:Guaka>`__) 14:14, 28
      March 2012 (UTC)

-  Debian Squeeze - this makes 2.6 easier to use, but I'd survive if
   it's deprecated. (Would consider moving to Debian Wheezy, which is
   currently Testing, or running a VM.)
   --`Chriswaterguy <User:Chriswaterguy>`__
   (`talk <User talk:Chriswaterguy>`__) 15:52, 20 March 2012 (UTC)
-  I also would like to keep this version supported until debian stops
   using this version in the current version. I wouldn't mind an upgrade
   to python3, this can also be installed and is supported in de latest
   debian. - `Warddr <User:Warddr>`__ (`talk <User talk:Warddr>`__)
   23:01, 8 April 2012 (UTC)
-  Host which I use is running Debian Squeeze and they won't update
   Python until Debian does. --`Harriv <User:Harriv>`__
   (`talk <User talk:Harriv>`__) 07:36, 1 May 2012 (UTC)
-  debian stable support is very nice.
-  Using Debian Squeeze. I am not going to run backports on my server,
   and my 2.7 install lacks a few features -- in some cases, I'm mixing
   2.5, 2.6 and 2.7.
   `75.137.144.72 <Special:Contributions/75.137.144.72>`__ 05:26, 12 May
   2012 (UTC)
-  Using Ubuntu 10.04 (Lucid) (yes, I know it's old), which doesn't come
   with 2.7 (although it does come with 3 and 3.1...
   `JesseW <User:JesseW>`__ (`talk <User talk:JesseW>`__) 23:41, 16 May
   2012 (UTC)
-  CrunchBang Linux "Statler" based on Debian Squeeze
   `Kpjas <User:Kpjas>`__ (`talk <User talk:Kpjas>`__) 23:11, 21 May
   2012 (UTC)
-  I'm also using Cygwin for the most part - though I could migrate
   (with some hassle) to a cygwin-free setup.
   -`Avic <User:Avicennasis>`__ :sup:``talk? <User_Talk:Avicennasis>`__`
   05:33, 7 August 2012 (UTC)
-  Using Debian Squeeze. I am not going to run backports on my server.
   `DonPaolo <User:DonPaolo>`__ (`talk <User talk:DonPaolo>`__) 20:56,
   27 September 2012 (UTC)

Python 2.7.0/2.7.1 users
------------------------

*Edit this section if you have a serious reason to use this version of
Python*

-  fedora uses 2.7.1
-  toolserver uses 2.7.1 but patched to have unicode bug fixed
-  ubuntu uses 2.7.1+ (not sure what the "+" stands for, look e.g.
   `here <http://wiki.ubuntuusers.de/Python#Start>`__)

I think the day we can go officially to 2.7.2 will become a "delightful
holiday", but meanwhile this is slightly more radical than useful. The
2.7.1 seems to be a magic and commonly used one.
--`DrTrigon <User:DrTrigon>`__ (`talk <User talk:DrTrigon>`__) 12:37, 29
February 2012 (UTC)

"Not supported does not necessarily mean we have to actively remove bits
that work around quirks for a certain version; rather, it means we won't
fix bugs due to an old python version." - I would agree with that, since
we should not waste time in something that might become
contra-productive for some users. --`DrTrigon <User:DrTrigon>`__
(`talk <User talk:DrTrigon>`__) 12:59, 29 February 2012 (UTC)

    If you want to run an interwiki bot, you either have to use python
    2.5 or >= 2.7.2. In addition, recent releases of ubuntu (oneiric and
    precise) already use 2.7.2
    (`source <http://packages.ubuntu.com/search?keywords=python2.7>`__).
    `Valhallasw <User:Valhallasw>`__ (`talk <User talk:Valhallasw>`__)
    17:02, 8 March 2012 (UTC)

        I think we should cut a branch for 2.5 support, start
        refactoring code for 2.7.2 so it is available for any distro
        that includes 2.7.2 in their stable release. `John
        Vandenberg <User:John Vandenberg>`__
        (`talk <User talk:John Vandenberg>`__) 08:03, 10 March 2012
        (UTC)
        Sorry, I don't understand what you are suggesting. What code
        should be refactored, and how is this related tho whether the
        distro includes 2.7.2 in the stable release or not? In addition,
        I don't really see the point of branching - that would only
        /increase/ maintenance burden. `Valhallasw <User:Valhallasw>`__
        (`talk <User talk:Valhallasw>`__) 15:41, 11 March 2012 (UTC)

            I'm using natty 11.04 ubuntu, it's not ancient, it's the
            latest or close to it and has 2.7.1+
            `Penyulap <User:Penyulap>`__ (`talk <User talk:Penyulap>`__)
            20:36, 30 May 2012 (UTC)

`Survey2012 <Category:Pywikibot>`__
