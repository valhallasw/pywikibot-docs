.. raw:: mediawiki

   {{Template:Pywikipediabot}}

.. raw:: mediawiki

   {{Bothelp}}

How to report a bug
-------------------

When you `report a
bug <https://blog.wikimedia.org/2013/03/18/how-to-create-a-good-first-bug-report/>`__,
please try to include:

-  What Pywikipediabot version you are using. We recommend that you test
   if the bug is still present in `the latest available revision, as
   stored in
   Git <https://git.wikimedia.org/summary/pywikibot%2Fcore.git>`__.
-  Python version (do ``python -V`` to check) and operating system you
   use (e.g. Windows, Linux, Mac OS...).

   -  To do that, `version.py <Manual:Pywikipediabot/version.py>`__ will
      be useful.

-  A nice summary.
-  A full description of the problem/report.
-  How to reproduce the bug, with full information (script, command
   line, family, and language used).
-  The console output provided by the script (included the Python
   traceback if you are reporting a crash).

To submit a new bug, visit the `bug
tracker <https://bugzilla.wikimedia.org/buglist.cgi?bug_status=__open__&product=Pywikibot>`__.

Development
-----------

If you have thought of a function you want to have, and none of the bots
provides it yet, you can ask one of the programmers to write it for you.
Or even better, you can try to work on the bots yourself. Python is a
nice language, and not hard to learn. We will welcome you.

Commit access
~~~~~~~~~~~~~

Anyone can get `Developer access <Developer access>`__. Once you've
registered, if you're interested in working on pywikipedia, please email
`the mailing list <mail:Pywikipedia-l>`__ and introduce yourself and
mention what you'd like to work on, so other people can greet you.

Working with source code
~~~~~~~~~~~~~~~~~~~~~~~~

{{\|Manual:Pywikibot/Gerrit\|Gerrit/TortoiseGit tutorial}}

-  How to submit patches: configure Git and Gerrit. Follow steps in
   `Gerrit/Getting started <Gerrit/Getting started>`__ and run this:

.. code:: bash

    #for hacking core
    git clone ssh://USERNAME@gerrit.wikimedia.org:29418/pywikibot/core.git

and after modifying the code, follow the steps in
`Gerrit/Tutorial <Gerrit/Tutorial>`__.

Example (step-by-step)
~~~~~~~~~~~~~~~~~~~~~~

So for example if you want to work with **compat** (formerly known as
**trunk**), do the following, step-by-step:

#. `setup your software <Gerrit/Getting started>`__:

   #. if not done already for svn [1]_ access; create an *SSH key*, a
      *developer account* and *add your public key* to gerrit as well as
      to wikitech
   #. install 'git' package
   #. install 'git-review' package (the one by openstack
      `1 <https://pypi.python.org/pypi/git-review>`__, NOT the one by
      Facebook)

#. clone and setup your repo:

   #. clone the git [2]_ repo with all submodules by using (like
      ``svn checkout``)

$ git clone --recursive
ssh://USERNAME@gerrit.wikimedia.org:29418/pywikibot/compat.git
pywikipedia-git

.. raw:: html

   </source>

and wait, this step will take some time

#. 

   #. enter the directory

$ cd pywikipedia-git

.. raw:: html

   </source>

#. 

   #. config git setting for this repo/directory only (not global, in
      case e.g. you have different pseudo for multiple projects)

$ git config user.email "EMAIL"

.. raw:: html

   </source>

and

.. code:: bash

    $ git config user.name "USERNAME"

in order to configure this globally, use the ``--global`` parameter

#. 

   #. config your terminal/console to output english messages (in order
      to work properly with git review, see
      `Gerrit/git-review#Troubleshooting <Gerrit/git-review#Troubleshooting>`__)

$ alias git="LANG=C git"

.. raw:: html

   </source>

this has to be done every time a new console is started, in order to
configure this permanently, put this into your ``bashrc`` or similar
setup file

#. 

   #. setup git review for this repo only

$ git review -s

.. raw:: html

   </source>

and enter your ``USERNAME`` again, this is an important step - if you
forget it, according to `Gerrit/Tutorial#Push your change set to
Gerrit <Gerrit/Tutorial#Push_your_change_set_to_Gerrit>`__, the final
``git review`` below (needed to commit your changes for review) will
fail - though this can be still solved then

#. `work with the repo <Gerrit/Getting started>`__, e.g. commit patches
   for review:

   #. switch to the master branch (might not be needed)

$ git checkout master

.. raw:: html

   </source>

#. 

   #. update the current branch to revision online (like ``svn update``)

$ git pull

.. raw:: html

   </source>

#. 

   #. create your own local temporary branch for working

$ git checkout -b MEANINGFUL\_BRANCH\_NAME

.. raw:: html

   </source>

and try to choose a ``MEANINGFUL_BRANCH_NAME`` with the help of the
`branch naming tips <Gerrit/Tutorial#Create_a_branch>`__ available

#. 

   #. now write some code; see the `Git commands <Gerrit/Tutorial>`__
      add, rm and mv to add, remove or rename files - when you're ready
      go to the next step
   #. commit your changes to your local temporary branch with

$ git commit --all # In the Gerrit world you can do this only once per
branch! Remember to follow the commit message guidelines.

.. raw:: html

   </source>

(you can use ``-a`` instead of ``--all`` and ``-R`` instead of
``--no-rebase``) and, as used from svn, enter a meaningful commit
message, e.g. a short description of your code changes

#. 

   #. optionally, check your changes by looking at the committed data

$ git show HEAD

.. raw:: html

   </source>

and make sure that you are sending what you wanted to

#. 

   #. send the data to the online repository, resp. `gerrit for
      review <Gerrit/git-review#What_happens_when_you_submit_a_change>`__
      (like ``svn commit``)

$ git review

.. raw:: html

   </source>

#. 

   #. finally go to `Gerrit <https://gerrit.wikimedia.org>`__, click on
      your change and write a reviewer's name in the input box near the
      "Add Reviewer" button

Documentation
-------------

*This* is the user and developer manual, as can be found on
Manual:Pywikibot, please help keeping it updated.

The code itself is partly documented as well with help of
`doxygen <w:doxygen>`__. You can find them, e.g. at:

-  `compat <toollabs:drtrigonbot/docs/compat/html>`__
-  core (n/a yet)

as well as `unit test <w:unit test>`__ `code
coverage <w:code coverage>`__ reports at:

-  `compat <toollabs:drtrigonbot/docs/compat/coverage>`__
-  core (n/a yet)

Bot & Proxy
-----------

Core: Add the following lines to user-config.py:

.. code:: python

    import httplib2, socks
    proxy = httplib2.ProxyInfo(socks.PROXY_TYPE_HTTP, 'localhost', 8080)

Compat: Add the following line to your user-config.py:

.. code:: python

    proxy = {'host': 'localhost:8080', 'auth': None}

Debugging network issues
------------------------

See `Pywikibot/mitmproxy <Pywikibot/mitmproxy>`__ for tips.

See also
--------

-  (SVN) Code Review - MediaWiki:
   https://www.mediawiki.org/wiki/Special:Code/pywikipedia
-  (GIT) gerrit.wikimedia Code Review:
   https://gerrit.wikimedia.org/r/#/admin/projects/pywikibot

References
----------

.. raw:: html

   <references/>

`Development <Category:Pywikibot>`__

.. [1]
   Book: *Version Control with Subversion* for Subversion 1.7.
   http://svnbook.red-bean.com/

.. [2]
   Book: *Pro Git*. http://git-scm.com/book
