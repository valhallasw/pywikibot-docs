.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/Basic use}}

.. raw:: mediawiki

   {{Pywikibot}}

Use
---

    *See `Shortcut in command
    line <Manual:Pywikipediabot/Installation#Shortcut_in_command_line>`__
    for Windows users.*

Select and run a bot script
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now that you have installed python and Pywikipediabot, you need to get
to a textual interface to your Operating System.

Accessing pywikipedia

After you have created the file that is named
**`user-config.py <Manual:Pywikipediabot/user-config.py>`__**, you can
access pywikipedia.

On **Windows** this is done by opening the start menu, and clicking on
'Run'. You are asked to give the name of a program, type "cmd.exe".

-  Change the root to C: by typing chdir C:\\
-  Type chdir \\"name of the folder where pywikipedia bot has been
   `downloaded <Manual:Pywikipediabot/Installation>`__" *(For example:
   chdir \\"pywikipedia" if the file is in the C: folder.)*

On **Mac**, find Terminal.app in /Applications/Utilities, see `Mac
Installation <Manual:Pywikipediabot/Mac>`__.

On **Linux** or any other **Unix**, use any terminal application such as
gnome-terminal, konsole, xterm, or simply the text-mode console.

Run the script `login.py <Manual:Pywikipediabot/login.py>`__ by typing
"python login.py" (or just "login.py" for windows). If you don't have
``user-config.py`` yet, this command will interactively create it.

Entering password

Python will then return:

'''

::

    Password for user your_bot on your_site:en:

'''

Use the password you used for the bot's login name. Note that your input
will not be visible for privacy reasons. The bot can't work anonymously.
Unless you change your password, you normally need to run this program
only once, the bot usually does not get logged off.

Using a bot

The bots are in the main pywikipedia folder when downloaded.

If necessary, use the command cd to go to the directory where the bot
files are saved.

Now run any of the bots here by typing "python botname.py" (If you are
using Windows, you can leave out "python").

Scripts
-------

    *Main page: Manual:Pywikipediabot/Scripts*

Command-line arguments
~~~~~~~~~~~~~~~~~~~~~~

Although many bot scripts have their own command line arguments, which
should be documented on their respective pages (or in their source
code), all bots unless specifically stated to the contrary recognize the
following command line arguments:

-help
    Print a list of global bot arguments (this list), followed by
    bot-specific help if available.
-lang:xx
    Set the language of the wiki you want to work on to language code
    ``xx``, overriding the configuration in ``user-config.py``.
-family:xyz
    Set the family of the wiki you want to work on, *e.g.*, wikipedia,
    wiktionary, wikitravel, ... This will override the configuration in
    ``user-config.py``.
-user:xyz
    Log in as user 'xyz' instead of the default username.
-log
    Enable the logfile. Logs will be stored in the logs subdirectory.
-log:xyz
    Enable the logfile, using ``xyz`` as the filename.
-nolog
    Disable the logfile (if it's enabled by default).
-putthrottle:nn
    Set the minimum time (in seconds) the bot will wait between saving
    pages. The default value is 10.

For example, ``python scriptname.py -family:wiktionary`` will run the
"scriptname" bot on wiktionary articles, overriding the default family
setting in your user configuration.

Permission on wikimedia projects
--------------------------------

Make sure that your bot is approved by the wiki community where you are
going to use it. Strictness of this differs greatly between various
projects; at some you need to announce it in advance and get approval
before you start, at others you can do whatever you want.

Using your normal browser, create a login name and password for the bot.
It is best to use a name that makes clear that it is a bot, and
preferably also who is operating it. A common method is to use your own
login name and add the word 'bot' to it, but several other forms also
exist.

On the English Wikipedia, bots are only allowed to be used if they are
approved at `Wikipedia:Bots/Requests for
approval <:en:Wikipedia:Bots/Requests for approval>`__.

Request a bot flag
^^^^^^^^^^^^^^^^^^

If you heavily use a bot, it will clutter recent changes. To avoid that,
you can get your bot registered as such. In that case it will not be
shown on Recent changes unless a user specifically asks to get bots
included.

This can be done by a `Bureaucrat <:en:Wikipedia:Bureaucrat>`__. You can
put a request to get your or someone else's bot registered at `Steward
requests/Bot status <:meta:Steward requests/Bot status>`__. You will
probably be asked for some kind of evidence that your local community
agrees with your bot. On the English language Wikipedia, requests should
be made at `Wikipedia:Bots/Requests for
approval <:en:Wikipedia:Bots/Requests for approval>`__. It is probably
good to get your bot registered whenever it will edit many pages in a
single run.

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/Basic use}}

`Basic use <Category:Pywikibot>`__
