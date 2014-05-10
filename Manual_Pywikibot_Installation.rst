Initial setup
-------------

There are four basic steps to installing pywikibot:

#. Download or update Python,
#. Decide which version to use,
#. Download pywikibot,
#. Configure pywikibot's basic settings.

Downloading Python
~~~~~~~~~~~~~~~~~~

Unix systems: typically have a recent-enough version of Python (2.5 for
compat, 2.6 for core) installed. Check with ``''python --version''``.

Mac OS X 10.8+: has a version of Python that is recent enough to run
pywikibot. If you run an older OS X, or are unsure, download and install
Python 2.7.6 from http://www.python.org/downloads/

Windows: download and install the latest release Python 2.7.6 from
http://www.python.org/downloads/

Python 3: Pywikibot currently does not work on Python 3. The support is
being implemented in **Core branch**

Two versions of pywikibot
~~~~~~~~~~~~~~~~~~~~~~~~~

There are two branches under active development. You can choose between:

-  **Core**, which should be your first choice. If you don't know what
   to choose, take this branch.
-  **Compat** (former "**trunk**\ ") is an older version of the
   framework. If you are editing on old wikis (pre-1.16 or so), or
   require one of the scripts that is not available on core yet (see the
   `compatibility list <../Scripts>`__), this is what you want.

.. raw:: mediawiki

   {{TNT|note}}

Due to an unicode bug of the underlying python library, python release
2.7.2 or higher is strictly recommended for Wikimedia projects with
Compat branch. See also the `requirements for a
bot <../Overview#Requirements_for_a_bot>`__, which gives a short
overview over needed python release and pywikibot branches.

Download Pywikibot
~~~~~~~~~~~~~~~~~~

The easiest way to download Pywikibot is to use
[\ http://tools.wmflabs.org/pywikibot/\  the latest nightly release].
Just download the pywikibot zip file to your computer and decompress the
file – there is no further installation required.

Download Pywikibot with Git
^^^^^^^^^^^^^^^^^^^^^^^^^^^

 {{\|Manual:Pywikipediabot/Gerrit}}

For installing with Git you need to run:

For core (formerly "rewrite")

.. code:: bash

    git clone --recursive https://gerrit.wikimedia.org/r/pywikibot/core.git

For compat (formerly "trunk")

.. code:: bash

    git clone --recursive https://gerrit.wikimedia.org/r/pywikibot/compat.git

with the ``--recursive`` option. It automatically install required
submodules. Currently there are two submodules (i18n and spelling); one
of them (i18n) is really required even for English language bots:

.. code:: bash

    #i18n
    git clone https://gerrit.wikimedia.org/r/pywikibot/i18n.git
    #<translate><!--T:14-->
    spellchecker database</translate>
    git clone https://gerrit.wikimedia.org/r/pywikibot/spelling.git 

Download Pywikibot with SVN
^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you don't want to use Git you can still use SVN.

Windows user may use the GUI extension TortoisSVN, see `next
section <#Download_Pywikibot_with_TortoiseSVN_for_Windows_user>`__
below.

For installing with SVN you should run

For core (formerly rewrite)

.. code:: bash

    svn co https://github.com/wikimedia/pywikibot-core/trunk core
    cd core/scripts
    svn co https://github.com/wikimedia/pywikibot-i18n/trunk i18n

For compat (formerly trunk)

.. code:: bash

    svn co https://github.com/wikimedia/pywikibot-compat/trunk compat
    cd compat
    svn co https://github.com/wikimedia/pywikibot-i18n/trunk i18n

Download Pywikibot with TortoiseSVN for Windows user
''''''''''''''''''''''''''''''''''''''''''''''''''''

TortoiseSVN is a Windows shell extension with GUI working as SVN client.
You may download the current release at
http://tortoisesvn.net/downloads.html. If you like using TortoiseSVN you
may use it as follows:

For core release (formerly rewrite)

#. Right-click on your prefered directory and execute
   ``"Start SVN checkout..."``
#. Choose ``"URL of repository"`` and paste the URL
   ``<tvar|pwb_core_github_svn>https://github.com/wikimedia/pywikibot-core/trunk</>``
#. Choose ``"Checkout directory`` and change the default directory which
   is ``<your prefered directory>/pywikibot-core`` e.g. to
   ``<your prefered directory>/svn-core`` if you like.
#. Confirm with ``[ OK ]``

    Now we have to install external libraries used by the framework.
    There are different ways to do that e.g. again with the checkout
    command. Another way is using properties. You may set it manually
    but it is very easy to use the preference file named *.svnprops*
    comming with the framework which sets all the needed properties:

#. Right-click your working directory
#. Select the last item in the drop list which might be folder's
   ``"Properties"``
#. Select ``"Subversion"`` tab and click on ``[ Properties... ]`` button
#. click ``[ Import... ]`` and select the file ``".svnprops"`` in your
   framework folder
#. Confirm with ``[ OK ]`` for property settings
#. Confirm with ``[ OK ]`` for folder properties
#. Now right-click onto your working copy and select ``"SVN update"`` to
   download the external libraries.

For compat release (formerly trunk)

#. Right-click on your prefered directory and execute
   ``"Start SVN checkout..."``
#. Choose ``"URL of repository"`` and paste the URL
   ``<tvar|pwb_compat_github_svn>https://github.com/wikimedia/pywikibot-compat/trunk</>``
#. Choose ``"Checkout directory`` and change the default directory which
   is ``<your prefered directory>/pywikibot-compat`` e.g. to
   ``<your prefered directory>/svn-compat`` if you like.
#. Confirm with ``[ OK ]``

    Now we have to install external libraries used by the framework.
    There are different ways to do that e.g. again with the checkout
    command. Another way is using properties in a similar way as in core
    release.

Updating the working copy

Right-click on your working copy and choose ``"SVN Update"``

Shortcut in command line
~~~~~~~~~~~~~~~~~~~~~~~~

To allow your source code to be developed outside of the pywikibot
source directory, add something like:

.. code:: bash

    PYTHONPATH=$PYTHONPATH:~/pywikipedia/
    export PYTHONPATH

 to a file that gets run on login, usually ~/.bashrc - this avoids
typing the export PYTHONPATH part in each time you log in. Naturally,
change paths to match your installation.

Similarly, you can set the PYWIKIBOT\_DIR environment variable to
specify the directory in which user-specific information is stored (in
particular, `user-config.py <Manual:Pywikipediabot/user-config.py>`__
which contains `login <Manual:Pywikipediabot/login.py>`__ data for the
bot).

Windows users: create a shortcut
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

How to make a quick shortcut to run commands (Windows users):

If you're installing Pywikibot in a folder such as "My Documents" it may
be troublesome to repeatedly use the "chdir" command to go into the
folder to run the bots.

On Windows you can create a shortcut which will open the command box
which you can use to run bots easily. Just follow these steps to create
one:

#. Right click the folder pywikibot is installed in.
#. Click "Create shortcut". A new shortcut icon with the arrow key will
   be created.
#. Right click on the new shortcut, and click properties.
#. In the properties window, in the target box type in **cmd.exe**.
#. In the "start in" box enter the full address of pywikibot.
#. Click "OK".
#. Click the shortcut and the cmd.exe opens up with the full path
   listed.

       If you press F5 to refresh the window (or re-open the shortcut's
       properties), you will notice that the shortcut icon has changed.

Updating
~~~~~~~~

The pywikibot framework is a perpetual beta software. Bugfixes, new
options, new behavior and changes of the mediawiki software leads to
frequently new releases and needs the working copy code to be up to
date. Please update your branch regularly (daily period or at least once
a week).

Updating nightly dump
^^^^^^^^^^^^^^^^^^^^^

-  If you are using a nightly version, the process is a bit more
   complicated. You have to re-download a full copy from
   [\ http://tools.wmflabs.org/pywikibot/\  here]. Before installing it,
   backup your configuration files and scripts (``user-config.py``, any
   family file, or custom script that you might have created, and any
   current dump xml file you're using for a wiki). Replace your
   pywikibot directory by the new version you just downloaded. Restore
   your configuration files. If you're not sure of what you're doing, do
   not erase but keep a backup of your complete old pywikibot directory,
   to avoid losing any important files.

.. raw:: mediawiki

   {{ {{TNTN|Note}} |1=If you have changed some scripts of the framework, you have to merge the differences by yourself. Version control systems like git or svn does it automatically.}}

Updating git
^^^^^^^^^^^^

-  If you used Git for downloading Pywikibot, you must go to the your
   directory and run the following command:

    .. code:: bash

        git pull --all

-  You may need to do
   .. code:: bash

       git submodule update

    as well, if you need up-to-date i18n files.

Automatic updating git on Wikimedia Labs or Toolserver
''''''''''''''''''''''''''''''''''''''''''''''''''''''

For automatic updating you can make **update** bash file and put it in
root and fill it with these commands, For WMF labs (in your service
group):

.. code:: bash

    #!/bin/bash
    cd /data/project/yourservicegroup/pywikipedia
    git pull --all && git submodule update

 and then run **crontab -e** and enter the following to make your bot to
run every day at 00:00AM (midnight):

.. code:: bash

    0 0 * * * bash /data/project/yourservicegroup/update >/dev/null 2>&1

 **Notice:** in these cods *yourservicegroup* is name of your service
group (without "-local").

For auto-updating in toolserver you just need to as the same as above
but instead of "/data/project/yourservicegroup/" you need to enter
"/data/project/yourusername/" which is "yourusername" is your user name!

Updating svn
^^^^^^^^^^^^

To update the code for core branch:

.. code:: bash

    svn up core/trunk
    cd core/scripts 
    svn up i18n

 To update the code for compat branch:

.. code:: bash

    svn up compat/trunk
    cd compat
    svn up i18n

Updating with TortoiseSVN (for Windows user)
''''''''''''''''''''''''''''''''''''''''''''

Updating the working copy with TortoiseSVN is just easy: Right-click on
your working copy directory and choose ``"SVN Update"``

Dependencies
------------

The pywikibot framework is quite a big and complex code and some scripts
needs external python modules (libraries) from other sources also in
order to work properly. The dependencies can be installed manually or
automatically (not supported by core yet).

If any issues arise during installation (of dependencies) please `file a
bug report <Manual:Pywikipediabot/Development#How_to_report_a_bug>`__ or
write to the pywikipedia-l maillist.

Automatic (recommended)
~~~~~~~~~~~~~~~~~~~~~~~

If available this is the recommended way, because this will result in an
identical setup on all machines. All you have to do is just execute your
favorite script after installation and pywikibot will ask you whether
you want to install missing packages.

Packages will be installed from OS package management if possible (all
Linux, not under win). If they cannot be found they will be downloaded
as archive from original source, extracted and installed. In the course
of this process a few packages have to be slightly modified in order to
work seamlessly with pywikibot. This modification needs an additional
binary tool called `patch <w:en:Patch (Unix)>`__ (patch.exe under win).
Unfortunately this is not available from MS; however, we can use a port
of the original linux code
([\ http://gnuwin32.sourceforge.net/packages/patch.htm\  gnuwin32
patch.exe])

 It is worth mentioning here that - despite the OS package management
"install mode" - all files are installed *locally* into the
``externals/`` directory of pywikibot. This is a very useful feature for
users that do not have permission to install software to their system,
e.g. non-admins.

Manual (for experts)
~~~~~~~~~~~~~~~~~~~~

In order to install the needed packages manually, you first need to know
which ones. A full list of all needed modules can be found in
[\ https://git.wikimedia.org/blob/pywikibot%2Fcompat/553235e6fadaa27427b295bfa531b5904ad38f1a/externals%2F__init__.py
externals/\_\_init\_\_.py] and contains:

-  framework core code:

   -  i18n *[git submodule]*
   -  spelling *[git submodule]*
   -  httplib2 *[git submodule]*
   -  BeautifulSoup.py *[included since important]*
   -  patch.exe

-  

depending of which script will be used:

-  

   -  opencv, opencv/haarcascades *[git submodule]*
   -  pycolorname *[git submodule]*
   -  irclib
   -  mwparserfromhell
   -  parse-crontab
   -  odfpy
   -  openpyxl
   -  python-colormath
   -  jseg, jseg/jpeg-6b
   -  mlpy
   -  music21
   -  ocropus
   -  pydmtx
   -  py\_w3c
   -  zbar
   -  (slic)
   -  (bob, xbob\_flandmark)

 Which ones you really need, depends strongly on the script you intend
to run - if you are unsure use the automatic mode above. In order to
check correct installation just run a bot script. If the dependencies
are satisfied everything will be ok, else the framework will complain
and ask whether it should install missing packages automatically.

Setup on Wikimedia Labs/Tool Labs server
----------------------------------------

In order to install your bot onto the Wikimedia servers and run it from
there, make sure first to become familiar with `Wikimedia Labs/Tool
Labs <Wikimedia Labs/Tool Labs>`__ environment.

In the next step you have to request several accounts (for labs, for the
tools project, your tool), provide an ssh key and so on. How to do this
and then proceed, is described in full detail in `Setup pywikibot on
Labs <wikitech:DrTrigonBot#Setup_pywikibot_on_Labs>`__.

Pywikibot source repo moved (from svn) to git, please confer
Manual:Pywikipediabot/Gerrit first.

The `bots <wikitech:Nova Resource:Bots>`__ projects here has become
obsolete use `tools <wikitech:Nova Resource:Tools>`__ now, in order to
do so follow `Tools/Help <wikitech:Nova Resource:Tools/Help>`__ to get
an account. Then create your tool (service group).

If you used the toolserver in the past and know how everything used to
work there, confer `migrating from
toolserver <wikitech:User:Magnus_Manske/Migrating_from_toolserver>`__
for more info.

Now you are ready to start. Login to Labs tools project:

``$ ssh USERNAME@tools-login.wmflabs.org``

 switch to the tool account with

| ``maintainer@tools-login:~$ become ``\ *``toolname``*
| ``local-``\ *``toolname``*\ ``@tools-login:~$ ``

Now install/clone the pywikibot code to your tool account as described
below.

Install the bot code
~~~~~~~~~~~~~~~~~~~~

core
^^^^

Similar to the instructions given in
[\ http://lists.wikimedia.org/pipermail/pywikipedia-l/2013-August/008168.html\ 
this mail] do:

| ``$ git clone --recursive ``\ ```https://gerrit.wikimedia.org/r/pywikibot/core.git`` <https://gerrit.wikimedia.org/r/pywikibot/core.git>`__\ `` pywikibot-core``
| ``$ cd pywikibot-core ``

Now you have to setup pywikibot. Choose any one of the following
processes to configure your system:

-  Execute ``python generate_user_files.py``
-  Run your favorite bot script (e.g.
   ``python pwb.py clean_sandbox.py -simulate``) since you are doing
   this in a fresh clone, it will trigger a bunch of questions on how
   you want to configure your local copy, answer them carefully in order
   to proceed.
-  If you already have a config file(s) from a previous version, you can
   copy those existing files into the right places (e.g.
   pywikibot-compat/).

Further things you might have to to do (depending on what bot scripts
you want to run) is to setup all externals properly - which still has to
be done manually in *core*

| ``$ cd externals``
| ``$ cat READM ``

 and follow the instructions there.

You will also have to enter the password for your bot eventually.

Now you have finished the configuration of *core* and can continue
setting up the jobs to execute.

compat
^^^^^^

Do:

``$ git clone --recursive ``\ ```https://gerrit.wikimedia.org/r/pywikibot/compat.git`` <https://gerrit.wikimedia.org/r/pywikibot/compat.git>`__\ `` pywikibot-compat``

Now, as similarly described in the
`core <Manual:Pywikipediabot/Installation#core>`__ section above, you
have to setup pywikibot. Choose any one of the following processes to
configure your system:

-  Execute ``python generate_user_files.py``
-  Run your favorite bot script (e.g.
   ``python pwb.py clean_sandbox.py -simulate``) since you are doing
   this in a fresh clone, it will trigger a bunch of questions on how
   you want to configure your local copy, answer them carefully in order
   to proceed.
-  If you already have a config file(s) from a previous version, you can
   copy those existing files into the right places (e.g.
   pywikibot-compat/).

See `this article <Manual:Pywikibot/Quick_Start_Guide#Steps>`__ for more
details on configuring your bot including creating the files manually.
You may setup all externals manually if you want - but this is not
needed in *compat*, confer
Manual:Pywikipediabot/Installation#Dependencies for further info.

You will also have to enter the password for your bot eventually.

Now you have finished the configuration of *compat* and can continue
setting up the webspace and jobs to execute.

Setup the webspace
~~~~~~~~~~~~~~~~~~

Per default, the directory listing on http://tools.wmflabs.org/TOOLNAME
is disabled. If you want to allow it for all users, login to your tool
account (as already described) and

| ``$ cd ~/public_html``
| ``$ echo Options +Indexes >> .htaccess ``

If you run a bot with the ``-log`` option, you will find the log files
within the ``logs/`` directory. If you want to allow users to access it
from the web, do

| ``$ cd ~/public_html``
| ``$ mkdir logs``
| ``$ cd logs``
| ``$ ln -s ~/pywikibot-core/logs cor ``

If you want a specific file type to be handled differently by your
browser, e.g. ``.log`` files like text files, use (confer
[\ https://wikitech.wikimedia.org/w/index.php?title=Help:Move_your_bot_to_Labs&direction=prev&oldid=69904\ 
this])

``$ echo AddType text/plain .log >> .htaccess``

 and (don't forget to) clear your browsers cache afterwards.

Next you might want to consider you ``cgi-bin`` directory

``$ cd ~/cgi-bin``

 follow the hints given at `wikitech:Nova
Resource:Tools/Help#Logs <wikitech:Nova Resource:Tools/Help#Logs>`__
*exactly*, e.g. even the two commands

| ``$ /usr/bin/python      # valid``
| ``$ /usr/bin/env python  # in-vali ``

 work and do the same in shell, only the first one is valid and works
here, the second is invalid! Another point to mention is that `PHP
scripts go into public\_html, not
cgi-bin <wikitech:User:Magnus_Manske/Migrating_from_toolserver#PHP>`__.
Python scripts on the other hand `can be placed in public\_html or
cgi-bin <wikitech:Nova_Resource:Tools/Help#Published_directories>`__ as
you wish. I would recommend to use ``public_html`` for documents and
keep it listable, whereas ``cgi-bin`` should be used for CGI scripts and
be protected (not listable).

Setup the job submission
~~~~~~~~~~~~~~~~~~~~~~~~

In order to setup the submission of the jobs you want to execute and use
the grid engine you should first consider `wikitech:Nova
Resource:Tools/Help#Submitting, managing and scheduling jobs on the
grid <wikitech:Nova Resource:Tools/Help#Submitting,_managing_and_scheduling_jobs_on_the_grid>`__
and if you are familiar with the Toolserver and its architecture consult
`Migrating from
toolserver <wikitech:User:Magnus_Manske/Migrating from toolserver#qsub_et_al>`__
also.

In general labs uses SGE and its commands like ``qsub`` et al, this is
explained `in this
document <wikitech:Nova Resource:Tools/Help#Submitting,_managing_and_scheduling_jobs_on_the_grid>`__
which you should use in order to get an idea which command and what
parameters you want to use.

An `infinitely running
job <wikitech:Nova Resource:Tools/Help#Submitting_continuous_jobs_(such_as_bots)_with_'jstart'>`__
(e.g. irc-bot) like this (``cronie`` entry from TS submit host):

``06 0 * * * qcronsub -l h_rt=INFINITY -l virtual_free=200M -l arch=lx -N script_wui $HOME/rewrite/pwb.py script_wui.py -log``

 becomes

``$ jsub -once -continuous -l h_vmem=256M -N script_wui python $HOME/pywikibot-core/pwb.py script_wui.py -log``

 or shorter

``$ jstart -l h_vmem=256M -N script_wui python $HOME/pywikibot-core/pwb.py script_wui.py -log``

 the first expression is good for debugging. Memory values smaller than
256MB seam not to work here, since that is the minimum. If you
experience problems with your jobs, like e.g.

``Fatal Python error: Couldn't create autoTLSkey mapping``

you can try increasing the memory value - which is also needed here,
because this script uses a second thread for timing and this thread
needs memory too. Therefore use finally

``$ jstart -l h_vmem=512M -N script_wui python $HOME/pywikibot-core/pwb.py script_wui.py -log``

 Now in order to create a crontab follow `Scheduling jobs at regular
intervals with
cron <wikitech:Nova Resource:Tools/Help#Scheduling_jobs_at_regular_intervals_with_cron>`__
and setup for crontab file like:

``$ crontab -e``

and enter

| ``PATH=/usr/local/bin:/usr/bin:/bin``
| ``06 0 * * * jstart -l h_vmem=512M -N script_wui python $HOME/pywikibot-core/pwb.py script_wui.py -lo ``

Additional configuration
~~~~~~~~~~~~~~~~~~~~~~~~

Furthermore additional tools to support you and your bot at work are
available:

-  `wikitech:Nova
   Resource:Tools/Help#Backups <wikitech:Nova Resource:Tools/Help#Backups>`__,
   basically out-of-the-box but just for a short time period
-  `wikitech:Nova Resource:Tools/Help#Requesting a Gerrit/Git repository
   for your
   tool <wikitech:Nova Resource:Tools/Help#Requesting_a_Gerrit/Git_repository_for_your_tool>`__

   -  `Gerrit/New repositories#Step 3: Request space for your
      extension <Gerrit/New repositories#Step_3:_Request_space_for_your_extension>`__
   -  `Git/New repositories/Requests <Git/New repositories/Requests>`__

Additional configuration
------------------------

Creating user files
~~~~~~~~~~~~~~~~~~~

As last step before using the bot scripts, you have to create user
configuration files. There is a script to do this. Please refer to
`../generate user files.py <../generate user files.py>`__.

Running Pywikibot under Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Please notice the instruction at Manual:Pywikibot/Windows.

`Installation <Category:Pywikibot{{translation}}>`__
