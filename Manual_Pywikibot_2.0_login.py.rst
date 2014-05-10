The script included in ``scripts/login.py`` occasionally fails silently.
Until that is fixed, the following workaround can help: This sets the
PYWIKIBOT2\_DIR environment variable **before** importing pywikibot.

.. code:: python

    import os
    os.environ['PYWIKIBOT2_DIR'] = '/dir/that/contains/user-config.py/'
    import pywikibot
    site = pywikibot.Site()
    if not site.logged_in():
        site.login()  # If you've never logged in before, it may prompt you for a password

