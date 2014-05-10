.. raw:: mediawiki

   {{MoveToMediaWiki}}

.. raw:: mediawiki

   {{svn/pywikipedia}}

.. raw:: mediawiki

   {{Pywikibot|script}}

**Welcome.py** is a script of the `Pywikipedia
bot <Using the python wikipediabot>`__ framework used to welcome new
users. This script works out of the box for wikis that have been defined
in the script. It is currently used on the Dutch, Norwegian and Italian
Wikipedia, and Wikimedia Commons and English Wikiquote.

If you want download the latest version of this code use
`SVN <Using the python wikipediabot#Download_with_SVN>`__ or copy the
script from `this
wiki <http://botwiki.sno.cc/wiki/Python:Welcome.py>`__.

Ensure you have community support before running this bot!

URLs to current implementations
-------------------------------

-  Arabic Wikipedia: `w:ar:ويكيبيديا:سجل
   الترحيب <w:ar:ويكيبيديا:سجل الترحيب>`__
-  Wikimedia Commons: `commons:Commons:Welcome
   log <commons:Commons:Welcome log>`__
-  Dutch Wikipedia: `w:nl:Wikipedia:Logboek
   welkom <w:nl:Wikipedia:Logboek welkom>`__
-  English Wikiquote: `q:en:Wikiquote:Welcome
   log <q:en:Wikiquote:Welcome log>`__
-  Persian Wikipedia: `w:fa:ویکی‌پدیا:سیاهه
   خوشامد/امضاها <w:fa:ویکی‌پدیا:سیاهه خوشامد/امضاها>`__

Because of the fact that every project has different settings, the Bot
won't work if you don't put the right translation of the dictionaries
that are already in the script.

Description of basic functionality
----------------------------------

-  Request a list of new users every period (default: 3600 seconds)
-  Ignore local bot accounts and users with *bot* as part of his name
   which may be a global bot
-  Check if new user has passed a threshold for a number of edits
   (default: 1 edit)
-  Optional: check username for bad words in the username or if the
   username consists solely of numbers; log this somewhere on the wiki
   (default: False)
-  If user has made any edits, check if user has an empty talk page
-  If user had an empty talk page, add a welcome message
-  Optional: Once the set number of users have been welcomed, add this
   to the configured log page, one for each day (default: True)
-  If no log page exists, create a header for the log page first.

Parameters
----------

This script (by default not yet implemented) uses two templates that
need to be on the local wiki:

-  {{WLE}}: contains mark up code for log entries (just copy it from
   Commons)
-  {{welcome}}: contains the information for new users

This script understands the following command-line arguments:

::

        -edit[:#]      Define how many edits a new user needs to be welcomed
                       (default: 1, max: 50)

        -time[:#]      Define how many seconds the bot sleeps before restart
                       (default: 3600)

        -break         Use it if you don't want that the Bot restart at the end
                       (it will break) (default: False)

        -nlog          Use this parameter if you do not want the bot to log all
                       welcomed users (default: False)

        -limit[:#]     Use this parameter to define how may users should be
                       checked (default:50)

        -offset[:TIME] Skip the latest new users (those newer than TIME)
                       to give interactive users a chance to welcome the
                       new users (default: now)
                       Timezone is the server timezone, GMT for Wikimedia
                       TIME format : yyyymmddhhmmss

        -timeoffset[:#] Skip the latest new users, accounts newer than
                        # minutes

        -numberlog[:#] The number of users to welcome before refreshing the
                       welcome log (default: 4)

        -filter        Enable the username checks for bad names (default: False)

        -ask           Use this parameter if you want to confirm each possible
                       bad username (default: False)

        -random        Use a random signature, taking the signatures from a wiki
                       page (for instruction, see below).

        -file[:#]      Use a file instead of a wikipage to take the random sign.
                       If you use this parameter, you don't need to use -random.
                       
        -sign          Use one signature from command line instead of the default

        -savedata      This feature saves the random signature index to allow to
                       continue to welcome with the last signature used.

        -sul           Welcome the auto-created users (default: False)

        -quiet         Prevents users without contributions are displayed

Extra-functionality guide
-------------------------

Report, Bad Word and White List Guide:

#. Set in the code which page it will use to load the bad word list, the
   white list and the report.
#. In these pages you have to add a "tuple" with the names that you want
   to add in the two lists. For example: ('cat', 'mouse', 'dog'). You
   can also write other text in the page; it will work without problems.
#. What will the two pages do? Well, the Bot will check if a badword is
   in the username and set the "warning" to True. Then the Bot checks if
   a word of the white list is in the username. If yes, it removes the
   word and rechecks in the bad-word list to see if there are other bad
   words in the username.
#. **Example**:

   -  dio is a badword
   -  Claudio is a normal name
   -  The username is "Claudio90 fuck!"
   -  The Bot find dio and set "warning"
   -  The Bot find Claudio and set "ok"
   -  The Bot find fuck at the end and set "warning"
   -  Result: The username is reported.

#. When a user is reported you have to check him and do the following:

   -  If he's ok, put out the {{welcome}}
   -  If he's not, block him
   -  You can decide to put in a "you are blocked, change to another
      username" template or not.
   -  Delete the username from the page.

**Important**: The Bot checks the user in this order:

-  Searches to see if he has a talkpage (if yes, skip).
-  Searches to see if he's blocked, if yes he will be skipped.
-  Searches to see if he's in the report page, if yes he will be
   skipped.
-  If no, he will be reported.

Random sign guide
-----------------

-  Set the page that the bot will load
-  Add the signs in this way:

::

    *<white space>SIGN
    <new line>

**Example**:

.. code:: php

    <pre>
    * [[User:Filnik|Filnik]]
    * [[User:Rock|Rock]]
    </pre>

**Note**: The white space and <pre> </pre> aren't required but I suggest
you to use them.

Known issues/FIXMEs
-------------------

-  exits when wiki is down.
-  add variable for how many users to skip (f.e. the 10 latest users,
   that may not have made any edits)
-  use default pages if a wiki is not configured, so no configuration of
   the script would be required at all. Suggestion: use English language
   defaults.
-  The regex to load the user might be slightly different from project
   to project. (in this case, write to `Filnik <User:Filnik>`__ for
   help...)
-  If the User talk: translation has non-standard character it won't
   work.
-  Add in the report, the badword used to detect the user.

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/welcome.py}}

`welcome.py <Category:Pywikibot scripts>`__
