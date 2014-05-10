Pywikibot is currently moving to `Gerrit <Gerrit>`__! This is a simple
FAQ/how-to page on what you need to do.

Terminology
-----------

-  Git - a version control system. Replaces SVN.
-  Gerrit - a code review platform (http://gerrit.wikimedia.org).
   Replaces Special:CodeReview
-  compat - formerly known as "trunk". If you're not sure, you probably
   use this.
-  core - formerly known as "rewrite".

For users
---------

Git clients
~~~~~~~~~~~

-  Windows users: We recommend you use
   `TortoiseGit <https://code.google.com/p/tortoisegit/>`__
-  OSX/Linux: commandline git - http://git-scm.com/

For example in order to download core via commandline:

.. code:: bash

    git clone https://gerrit.wikimedia.org/r/pywikibot/core.git
    cd core
    git submodule update --init # Will fetch i18n
    cd externals
    git clone https://gerrit.wikimedia.org/r/pywikibot/spelling.git # Spelling files

To update:

.. code:: bash

    #Assuming we're already in "core"
    git pull
    git submodule update --force # Updates i18n messages

If you're lazy and want to be able to do that all at once, you can do:

.. code:: bash

    git config alias.pullall '!git pull && git submodule update --init --recursive'  # You only need to do this once.
    # Assuming  you're already in "core":
    git pullall # This updates everything

(copied from
`1 <http://stackoverflow.com/questions/4611512/is-there-a-way-to-make-git-pull-automatically-update-submodules>`__)
[add ``--global`` to make this alias stick for all projects]

Be noticed these codes might be of some size (for example compat is 170
MBs) because you're downloading the whole history of codes so if size of
codes are important for you (e.g. because of hard disk limits in servers
or low internet speed) you can simply clone shallow version of code, for
example this command downloads only the last three revisions:

.. code:: bash

    git clone --depth 3 https://gerrit.wikimedia.org/r/pywikibot/core.git

you can even cut this down to just the very last revision with
``--depth 1``. It is recommended to use ``--recursive`` in order to
include all externals/submodules also.

Using SVN
~~~~~~~~~

But wait... I don't want to use Git. Can I still use SVN? Yes! For this
example, I'm going to use pwb-core, however you can easily switch compat
in.

.. code:: bash

    svn co https://github.com/wikimedia/pywikibot-core/trunk
    cd core/scripts # If you're using compat, change this line to "cd compat"
    svn co https://github.com/wikimedia/pywikibot-i18n/trunk i18n

Updating is as simple as

.. code:: bash

    svn up core/trunk
    cd core/scripts # Again, compat is "cd compat"
    svn up i18n

.. raw:: mediawiki

   {{note}}

Windows users may also use the GUI extension *TortoiseSVN.* You'll find
the documentation
`here <../Installation #Download_Pywikibot_with_TortoiseSVN_for_Windows_user>`__.

URLs
~~~~

Your client will probably ask you for the repository url. The urls
follow the format of:
``https://gerrit.wikimedia.org/r/pywikibot/[repo name]``.

So for compat: ``https://gerrit.wikimedia.org/r/pywikibot/compat``.

So for core: ``https://gerrit.wikimedia.org/r/pywikibot/core``.

Nightly distributions
~~~~~~~~~~~~~~~~~~~~~

You can download the whole packages or browse the source code via
`nightly distributor in Wikimedia
Labs <http://tools.wmflabs.org/pywikibot/>`__

For developers
--------------

How to submit patches...configure git/gerrit. etc.

Follow steps in `Gerrit/Getting started <Gerrit/Getting started>`__ and
run this:

.. code:: bash

    #for hacking core
    git clone --recursive ssh://USERNAME@gerrit.wikimedia.org:29418/pywikibot/core.git

and after modifying codes follow steps in
`Gerrit/Tutorial <Gerrit/Tutorial>`__

Windows: Developer using Windows may also use `Gerrit/TortoiseGit
tutorial <Gerrit/TortoiseGit tutorial>`__ for further informations.

Example (step-by-step)
~~~~~~~~~~~~~~~~~~~~~~

So for example if you want to work with **compat** (formerly known as
**trunk**), do the following, step-by-step:

#. `setup your software <Gerrit/Getting started>`__:

   #. if not done already for svn access; create an *SSH key*, a
      *developer account* and *add your public key* to gerrit as well as
      to wikitech
   #. install 'git' package
   #. install 'git-review' package

      -  the one by openstack
         `2 <https://pypi.python.org/pypi/git-review>`__, NOT the one by
         Facebook
      -  any version like 1.12, 1.21, but `NOT
         v1.18 <Gerrit/git-review#"Could_not_parse_json_query_response:_u'Verified'">`__

#. clone and setup your repo:

   #. clone the git repo with all submodules by using (like
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
`branch naming tips <Gerrit/Tutorial#Create_a_branch>`__ available - the
branch can be removed when not needed anymore with
``git branch -D MEANINGFUL_BRANCH_NAME``

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

   #. optionally check your changes by looking at the committed data

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
      your change and write a reviewer name in the input box near the
      "Add Reviewer" button

$ git config filter.rcs-keywords.smudge 'maintenance/rcs-keywords.py %f'

.. raw:: html

   </source>

.. code:: bash

    $ git config filter.rcs-keywords.clean 'maintenance/rcs-keywords.py'

#\*\* for core (rewrite):

.. code:: bash

    $ git config filter.rcs-keywords.smudge 'rcs-keywords.py %f'

.. code:: bash

    $ git config filter.rcs-keywords.clean 'rcs-keywords.py'

#\*\* (may be we should consider using the `git-rcs-keywords
module <https://github.com/turon/git-rcs-keywords>`__ as mentioned in
`dealing-with-svn-keyword-expansion-with-git-svn <http://stackoverflow.com/questions/62264/dealing-with-svn-keyword-expansion-with-git-svn/5633162#5633162>`__)

Problems, issues and work-a-rounds
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

jenkins-bot messages
^^^^^^^^^^^^^^^^^^^^

```https://integration.wikimedia.org/ci/job/pywikibot-core-pep8/46/console`` <https://integration.wikimedia.org/ci/job/pywikibot-core-pep8/46/console>`__\ `` : FAILURE in ?s (non-voting)``

The patchset committed did not pass PEP8 code style checks. That says
nothing about the functionality of the code but about the style.

```https://integration.wikimedia.org/ci/job/pywikibot-core-pyflakes/46/console`` <https://integration.wikimedia.org/ci/job/pywikibot-core-pyflakes/46/console>`__\ `` : FAILURE in ?s (non-voting)``

The patchset committed did not pass pyflakes code style checks. That
says nothing about the functionality of the code but about the style.

``This change could not be automatically merged with the current state of the repository. Please rebase your change and upload a new patchset.``

The pachset cannot be merged automatically into current HEAD. Please
**consider `Gerrit/Advanced usage#Build failed due to merge
conflict <Gerrit/Advanced usage#Build_failed_due_to_merge_conflict>`__
for a solution**.

More info about this can be found in `Gerrit/Tutorial#How to submit a
patch <Gerrit/Tutorial#How_to_submit_a_patch>`__ and
`Gerrit/Tutorial#git review complains about multiple
commits <Gerrit/Tutorial#git_review_complains_about_multiple_commits>`__.

`Gerrit <Category:Pywikibot>`__
