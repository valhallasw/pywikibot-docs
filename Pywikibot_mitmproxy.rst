Guide to debugging pywikibot/core network issues using mitmproxy

`mitmproxy <http://mitmproxy.org/>`__ is a "man-in-the-middle proxy"
that allows you to intercept HTTP *and* HTTPS traffic - the latter by
forging SSL certificates. This is incredibly useful for debugging
pywikibot network issues, especially because tools such as ethereal are
incapable of sniffing the HTTPS traffic. In addition, mitmproxy allows
tampering with the traffic, allowing you to fake network errors.

Unfortunately, the mitmproxy version bundled with Ubuntu (aptitude
install mitmproxy) is too old -- the SSL certificate forging does not
work correctly. Instead, you will have to install it in a virtual
environment:

.. code:: bash

    $ virtualenv --system-site-packages mitmproxy 
    $ source mitmproxy/bin/activate
    $ pip install mitmproxy

This will install the most recent version of mitmproxy in that virtual
environment. To start it, use

.. code:: bash

    $ source mitmproxy/bin/activate
    $ mitmproxy

Now that mitmproxy is running, we need to configure pywikibot. There are
two things we need to change:

#. Traffic needs to pass through the proxy. For this, we use the
   ``proxy`` directive
#. We need httplib2 to accept the forged certificate. We therefore tell
   it to accept mitmproxy as certificate authority.

We achieve this by adding the following lines to user-config.py:

.. code:: python

    import httplib2, socks
    httplib2.CA_CERTS = os.path.expanduser("~/.mitmproxy/mitmproxy-ca-cert.pem")
    proxy = httplib2.ProxyInfo(socks.PROXY_TYPE_HTTP, 'localhost', 8080)
    del httplib2
    del socks

