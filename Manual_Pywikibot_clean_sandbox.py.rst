 `clean sandbox.py <category:Pywikibot scripts>`__ **clean\_sandbox.py**
is a simple script that automatically reverts the page Project:Sandbox
to a "clean" state, `replacing the text <#Replacement_text>`__ on the
page with a predefined message. This message is found within the file
``clean_sandbox.py`` within the ``pywikipedia`` folder on your computer.

Usage
-----

Using clean\_sandbox.py is exceedingly easy. Just type

::

    python clean_sandbox.py

If you wish, you can add a couple of arguments to the base instruction:

::


        -hours:#       Use this parameter if to make the script repeat itself
                       after # hours. Hours can be defined as a decimal. 0.01
                       hours are 36 seconds; 0.1 are 6 minutes.

        -delay:#       Use this parameter for a wait time after the last edit
                       was made. If no parameter is given it takes it from
                       hours and limits it between 5 and 15 minutes.
                       The minimum delay time is 5 minutes.

There isn't much point to running this script manually. Since it only
works on one page, you could accomplish the same task just as easily by
going into the sandbox page history and undoing to the last point where
the page was clean. However, if you keep one python window open on your
computer at all times, and you commit it to running this script once
every 12 hours with a certain amount of delay, it's then possible to
automatically clean your sandbox, regularly and in a way that waits
until it appears like no one is using the sandbox. A reasonable command
would therefore be:

    ``python clean_sandbox.py -hours:12 -delay:15``

Replacement text
----------------

By default, clean\_sandbox.py comes with a number of predefined messages
in various languages. If you look in your computer's ``pywikipedia``
file, you'll find a file called ``clean_sandbox.py``. Open that file and
you'll be exploring the actual script itself.

At the top of the file, in the area that says, ``content = {``, you'll
see a series of messages. The English language message can be found to
the right of the letters ``'en' :`` If you wish to change the message,
do so. Otherwise, make note of the template that is being called and
make sure that your wiki has a template with exactly that same name.
That template should contain a message about the rules or instructions
your wiki has for the use of the sandbox page.

Good names for the template include, but are not limited to, , and the
like.

To reiterate, the template named next to ``'en':`` must exactly match
the name of your sandbox header template for this script to work
correctly.
