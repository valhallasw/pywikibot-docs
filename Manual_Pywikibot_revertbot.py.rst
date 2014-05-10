 `revertbot.py <category:Pywikibot scripts>`__ **revertbot.py** is a
script that helps you clean up after your bot if it does undesirable
things. It goes through your bot's list of contributions, from most
recent to most ancient, and reverts the last revision your bot made on
each page — provided, of course, that your bot made the most recent
revision on the page.

**It is therefore most effectively used *immediately* after you notice
your bot has gone astray.**

Usage
-----

It is invoked by typing ``python revertbot.py``, and it appears to have
no parameters, options or other settings.

It should almost certainly not be run unattended, as it does not ask
permission to make changes. In at least version 7957 from February 2010,
its default — and unalterable — mode is just to automatically make
changes.
