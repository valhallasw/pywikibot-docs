``THIS PAGE IS A DRAFT AT THE MOMENT - THIS HAS FIRST TO BE DISCUSSED AND AGREED ON.``

Guidelines for pywikibot development that every developer has to agree
to. Every developer promises to follow and not to break them
intentionally.

If you need to break the rules or guidelines listed here, you have to
request and discuss a change in advance (as described below).

Users
-----

-  How to become an *user*?

   -  Agree to the license and clone the git repo in order to use the
      software.

-  How to become a *developer*?

   -  Be an advanced user. Introduce yourself and explain why you would
      like to become a developer on the maillist. Even better if you
      already provided some bug reports, feature requests or patches in
      advance. The active developers will discuss your admission - if
      there are no objections you will be accepted and added to the
      developer list.

-  How to become an *admin*?

   -  Become an (absolutely) essential developer through your work -
      e.g. commits - and you will be added sooner or later.

Repository
----------

-  Mediawiki GIT repository with Gerrit.
-  structure

   -  `pywikibot <https://gerrit.wikimedia.org/r/#/admin/projects/?filter=pywikibot>`__

      -  ``pywikibot/compat``: Code Version 1.0 - under active
         development.
      -  ``pywikibot/core``: Coder Version 2.0 - under active
         development.
      -  ``pywikibot/externals/???``: Forks of external code - NOT
         maintained by us. e.g. httplib2.
      -  ``pywikibot/???``: Submodules of code needed by pywikibot -
         maintained by us. e.g. i18n, opencv, pycolorname, sf-export,
         spelling

-  ...

Code
----

-  general

   -  `PEP 20 -- The Zen of
      Python <http://www.python.org/dev/peps/pep-0020/>`__

-  style

   -  `PEP 8 -- Style Guide for Python
      Code <http://www.python.org/dev/peps/pep-0008/>`__
   -  (more?)

-  structure

   -  Installation: Compat must not need to be installed. Core is
      designed as module to be installed, but can be used without also.
   -  Syntax: The syntax of compat will be adopted to the one of core
      (vice-versa if really needed only) in order to be able to use bot
      script with no or just minimal changes.
   -  Directories: Compat mixes framework and bot scripts in one
      directory (should be separated because of "Syntax"). Core must
      have a proper and clean directory structure.

-  compatibility

   -  All framework parts have to run on linux/unix (fedora, ubuntu,
      ...?), mac and win. Bot scripts should if possible (common ones
      like interwiki.py have to).

-  ...

Guidelines/Rules
----------------

-  This guidelines in the current form [DATE?] have to be approved by
   *all* active developers through, e.g. announcement on the maillist.
-  This guidelines can be changed at any time. First the change has to
   be announced on the maillist and all active developers have to agree
   on it. If none of them raises objections or puts a veto the changes
   can take effect.

`Guidelines <Category:Pywikibot>`__
