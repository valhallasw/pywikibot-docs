The **archivebot.py** is a script to archive discussion pages.

How it works?
-------------

The bot examines backlinks (Special:Whatlinkshere) to the requested
page(s). It then goes through all pages (or a specific page if specified
using options) and archives old discussions. This is done by breaking a
page into threads, then scanning each thread for timestamps. Threads
older than a specified threshold are then moved to another page (the
archive), the name of which can be based on either the thread's name or
a counter that is incremented when the archive reaches a certain size.

Parameters
----------

.. raw:: html

   <div style="background: #99B3FF; color: black; border: #668CFF solid 0.2em; padding: 0.85em; margin-left: 3em; margin-top: 0.5em; margin-right: 3em; margin-bottom: 0.5em;">

::

    Usage: archivebot.py [options] [LINKPAGE(s)]

    Options:
      -h, --help            show this help message and exit
      -f FILE, --file=FILE  load list of pages from FILE
      -p PAGE, --page=PAGE  archive a single PAGE
      -n NAMESPACE, --namespace=NAMESPACE
                            only archive pages from a given namespace
      -s SALT, --salt=SALT  specify salt
      -F, --force           override security options
      -c PAGE, --calc=PAGE  calculate key for PAGE and exit
      -l LOCALE, --locale=LOCALE
                            switch to locale LOCALE
      -L lang, --lang=lang  current language code
      -T TIMEZONE, --timezone=TIMEZONE
                            switch timezone to TIMEZONE
      -S --simulate         Do not change pages, just simulate

.. raw:: html

   </div>

| 
| 

`archivebot.py <Category:Pywikibot scripts>`__
