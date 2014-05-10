 `lonelypages.py <category:Pywikibot scripts>`__ **lonelypages.py** is a
bot that labels pages which are currently unlinked by other pages — in
other words, pages which appear on Special:LonelyPages. To accomplish
this, it places on a page, and substitutes some `magic
word <magic word>`__ dating, so that you know when you've added the
template. What your wiki gets out of this very much depends on how
you've coded .

Syntax and usage
----------------

Usage is incredibly straightforward. Just type
``python lonelypages.py``. That's it! No parameters or arguments to fuss
with. It will then go through the main namespace and find lonely pages
on which to place the template. If it encounters a page where the
template is already in place, it will go on to the next page.

Why do I need this?
-------------------

You may not. It depends on how much you *care* about lonely pages on
your wiki, or if you think it's worthwhile to use a bot to accomplish
this task. Wikipedia, for instance, do think it's important to tell
their users that a certain page is un-referenced elsewhere on their
project, but they adamantly don't want a bot to place the template. So
for Wikipedians, this bot has no value. They say that there are some
pages which are *always* going to be lonely, and they only want
{{tl\|orphan}] on pages where there's a reasonable prospect of future
linkage.

However, if your wiki community believes that *all* pages can
potentially be linked, then there's no reason whatsoever *not* to use a
bot. You can have your wiki patrolled in no time!

Still, some might wonder why this is needed when Special:LonelyPages
exists? A good rationale, though not the only one, is that many new
editors aren't aware that the "special" namespace even exists. Fewer
still will have navigated to Special:LonelyPages. And almost no one will
have actually waded through all the pages there. Placing a template on a
lonely page is a much more immediate way of alerting users to a problem
than relying on a page in the "special" namespace.

How do I code 
--------------

That's really up to you and your community. Wikipedia's version of the
template can be seen at wikipedia:template:orphan. But it can be done in
any way, really. Some wikis use the template merely to insert a
category. Some use it to create detailed categories that track lonely
pages by the month and date on which the template was placed. Because
this script places a category, the true potential of the script lies in
the hands of the person coding the template.
