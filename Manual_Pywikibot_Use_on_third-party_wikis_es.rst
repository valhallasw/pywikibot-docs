.. raw:: mediawiki

   {{languages|Manual:Pywikibot/Use on third-party wikis}}

    '' Si usted necesita más ayuda en la fundación de su pywikipediabot
    usted puede venir para la ayuda sobre [irc: //
    irc.freenode.net/pywikipediabot \*pywikipediabot] freenode el
    servidor. "

El bot `pywikipedia <Manual:Pywikipediabot/es>`__ puede ser usado para
hacer toda clase de cosas importantes para el mantenimiento de un
proyecto en `MediaWiki <MediaWiki/es>`__. Cuando este software es usado
fuera de los proyectos `Wikimedia <Wikimedia>`__ tienen que ser hechas
algunas configuraciones.

Algunos proyectos que no son de Wikimedia, "o familias", ya son apoyados
y están en la carpeta "de familias" en la cual usted puede
`dercargar <Using_the_python_wikipediabot#Download>`__. Usando los
archivos existentes como ejemplos, debería ser fácil adaptar el bot a su
propio proyecto. (Simplemente modifique los archivos existentes, o cree
un nuevo archivo en un archivo notebook.txt, salvando(ahorrando) el
archivo en la carpeta de familias, con un nombre como
`` mediawiki_family.py ``)

Ejemplos de familias
--------------------

Ejemplo: Mozilla wiki
~~~~~~~~~~~~~~~~~~~~~

Wiki de la Fundación Mozilla, wiki.mozilla.org, es un ejemplo muy simple
porque está sólo disponible en una lengua.

Esto es el contenido de families/mozilla\_family.py. Las insinuaciones
para usted para escribir su una especificación de familia son
subrayadas.

ejemplo del codigo:

.. code:: python

    # -*- coding: utf-8  -*-
    import family

    # The official Mozilla Wiki. #Put a short project description here.

    class Family(family.Family):

        def __init__(self):
            family.Family.__init__(self)
            self.name = 'mozilla' #Set the family name; this should be the same as in the filename.
            self.langs = {
                'en': 'wiki.mozilla.org', #Put the hostname here.
            }
            self.namespaces[4] = {
                '_default': u'MozillaWiki', #Specify the project namespace here. Other
            }                               #namespaces will be set to MediaWiki default.

            self.namespaces[5] = {
                '_default': u'MozillaWiki talk',
            }

        def version(self, code):
            return "1.4.2"  #The MediaWiki version used. Not very important in most cases.

        def path(self, code):
            return '/index.php' #The path of index.php

Ejemplo: Alfa de Memoria
~~~~~~~~~~~~~~~~~~~~~~~~

'' memoryalpha\_family.py '' es la definición "de familia" de Alfa de
Memoria, www.memory-alpha.org, un Viaje de Estrella wiki. Esta
especificación es un poquito más difícil porque esto tiene varia lengua

ejemplo del codigo:

.. code:: python

    # -*- coding: utf-8  -*-
    import family

    # The Memory Alpha family, a set of StarTrek wikis.

    class Family(family.Family):
        def __init__(self):
            family.Family.__init__(self)
            self.name = 'memoryalpha'

            self.langs = {  #All available languages are listed here.
                'de': None, #Because the hostname is the same for all languages,
                'en': None, #we don't specify it here, but below in the hostname()
                'nl': None, #function.
                'sv': None,
            }

            # Most namespaces are inherited from family.Family.
            self.namespaces[4] = {
                '_default': u'Memory Alpha', #All languages use the same project namespace name.
            }
            self.namespaces[5] = {
                '_default': u'Memory Alpha talk',
                'de': u'Memory Alpha Diskussion',
                'nl': u'Overleg Memory Alpha',
                'sv': u'Memory Alphadiskussion',
            }

            # A few selected big languages for things that we do not want to loop over
            # all languages. This is only needed by the titletranslate.py module, so
            # if you carefully avoid the options, you could get away without these
            # for another wiki family.
            self.biglangs = ['en', 'de'] #Not very important

        def hostname(self,code):
            return 'www.memory-alpha.org' #The same for all languages

        def path(self, code):
            return '/%s/index.php' % code #The language code is included in the path

        def version(self, code):
          return "1.4"

Ejemplo: Uncyclop æ dia
~~~~~~~~~~~~~~~~~~~~~~~

El vario `Uncyclop æ dias <wikia:c:uncyclopedia:Babel:Main_Page>`__ son
ligeramente más torpe como no reciben todos en el mismo dominio o bajo
el mismo nombre. Los nombres de dominio y caminos deben ser
especificados individualmente. El más son `Wikia <Wikia:Main_Page>`__ -
recibido a excepción de fi: hu: ja: no: punto: sv: y zh-tw:. Unos tienen
sus propios nombres de dominio certificados y la Lengua inglesa
`Uncyclopedia <wikipedia:Uncyclopedia>`__ también usa un número de
costumbre namespaces.

Los accesos que trabajan para un Uncyclop æ dia o un proyecto de Alfa de
Memoria típicamente pueden ser adaptados a otro Wikia.

" Note: Hubo actualizaciones subsecuentes y cambios, ven
wikia:c:uncyclopedia:es:usuario:Chixpy/uncyclopedia_family.py para la
versión corriente del Uncyclopedia interwiki bot la configuración. Allí
también son inresueltos publicaciones(cuestiones) en las cuales algunas
lenguas interwiki no están disponibles de todos los proyectos de
Uncyclopedia; proceda con precaución. "

.. code:: python

    # -*- coding: utf-8  -*-
    import family
        
    # The Uncyclopaedia family, a satirical set of encyclopaedia wikis.
    #        
    # Save this file to families/uncyclopedia_family.py in your pywikibot installation       
    # The pywikipediabot itself is available for free download from sourceforge.net          
    #

    class Family(family.Family):
        def __init__(self):
            family.Family.__init__(self)
            self.name = 'uncyclopedia'
        
            self.langs = {
            'ar': 'beidipedia.wikia.com',
                'ca': 'valenciclopedia.wikia.com',
                'da': 'da.uncyclopedia.wikia.com',
                'de': 'de.uncyclopedia.wikia.com',
                'el': 'anegkyklopaideia.wikia.com',
                'en': 'uncyclopedia.org',
                'es': 'inciclopedia.wikia.com',
                'fi': 'peelonet.zapto.org',
                'fr': 'desencyclopedie.com',
            'he': 'eincyclopedia.wikia.com',
                'hu': 'hu.uncyclopedia.info',
            'it': 'nonciclopedia.wikia.com',
                'ja': 'ja.uncyclopedia.info',
            'la': 'uncapaedia.wikia.com',
                'no': 'ikkepedia.net',
                'pl': 'nonsensopedia.wikia.com',
                'pt': 'pt.uncyclopedia.info',
                'ru': 'absurdopedia.net',
            'sv': 'psyklopedin.hehu.se',
            'zh': 'zh.uncyclopedia.wikia.com',
                'zh-tw': 'zh.uncyclopedia.info',
                }
        
            # Most namespaces are inherited from family.Family.
            self.namespaces[1] = {
                '_default': u'Talk',
                'ar': u'نقاش',
            'ca': u'Discussió',
            'da': u'Diskussion',
                'de': u'Diskussion',
                'el': u'Συζήτηση',
                'en': u'Talk',
            'es': u'Discusión',
            'fi': u'Keskustelu',
                'fr': u'Discuter',
                'he': u'שיחה',
            'it': u'Discussione',
            'la': u'Disputatio',
            'no': u'Diskusjon',
                'pl': u'Dyskusja',
                'pt': u'Discussão',
                'ru': u'Обсуждение',
            'sv': u'Diskussion',
                'zh-tw': u'討論',
        }

            self.namespaces[2] = {
                '_default': u'User',
                'ar': u'مستخدم',
            'ca': u'Usuari',
                'da': u'Bruger',
                'de': u'Benutzer',
                'el': u'Χρήστης',
                'en': u'User',
            'es': u'Usuario',
            'fi': u'Käyttäjä',
                'fr': u'Utilisateur',
                'he': u'משתמש',
            'it': u'Utente',
            'la': u'Usor',
            'no': u'Bruker',
                'pl': u'Użytkownik',
                'pt': u'Usuário',
                'ru': u'Участник',
            'sv': u'Användare',
            'zh-tw': u'用戶',
            }

            self.namespaces[3] = {
                '_default': u'User talk',
                'ar': u'نقاش المستخدم',
            'ca': u'Usuari Discussió',
                'da': u'Bruger diskussion',
                'de': u'Benutzer Diskussion',
                'el': u'Συζήτηση χρήστη',
                'en': u'User talk',
            'es': u'Usuario Discusión',
            'fi': u'Keskustelu käyttäjästä',
                'fr': u'Discussion Utilisateur',
                'he': u'שיחת משתמש',
            'it': u'Discussioni utente',
            'la': u'Disputatio Usoris',
            'no': u'Brukerdiskusjon',
                'pl': u'Dyskusja użytkownika',
                'pt': u'Usuário Discussão',
                'ru': u'Обсуждение участника',
            'sv': u'Användardiskussion',
            'zh-tw': u'用戶討論',
            }

            self.namespaces[4] = {
                '_default': u'Uncyclopedia',
            'ar': u'ويكيبيديا',
            'ca': u'Valenciclopèdia',
                'da': u'Spademanns Leksikon',
                'de': u'Uncyclopedia',
            'el': u'Ανεγκυκλοπαίδεια',
                'en': u'Uncyclopedia',
                'es': u'Inciclopedia',
            'fi': u'Hikipedia',
                'fr': u'Désencyclopédie',
                'he': u'איןציקלופדיה',
            'it': u'Nonciclopedia',
            'la': u'Uncapaedia',
            'no': u'Wikipedia',
                'pl': u'Nonsensopedia',
                'pt': u'Desciclopédia',
            'ru': u'Абсурдопедия',
            'sv': u'Psykelopedia',
            'zh': u'伪基百科',
            'zh-tw': u'偽基百科',
            }
            self.namespaces[5] = {
                '_default': u'Uncyclopedia talk',
            'ar': u'نقاش ويكيبيديا',
            'ca': u'Valenciclopèdia Discussió',
                'da': u'Spademanns Leksikon diskussion',
                'de': u'Uncyclopedia Diskussion',
            'el': u'Ανεγκυκλοπαίδεια συζήτηση',
                'en': u'Uncyclopedia talk',
                'es': u'Inciclopedia Discusión',
            'fi': u'Keskustelu Hikipediasta',
                'fr': u'Discussion Désencyclopédie',
                'he': u'שיחת איןציקלופדיה',
            'it': u'Discussioni Nonciclopedia',
            'la': u'Disputatio Uncapaediae',
            'no': u'Wikipedia-diskusjon',
                'pl': u'Dyskusja Nonsensopedia',
                'pt': u'Desciclopédia Discussão',
            'ru': u'Обсуждение Абсурдопедии',
            'sv': u'Psykelopediadiskussion',
            'zh': u'伪基百科 talk',
            'zh-tw': u'偽基百科討論',
            }

        self.namespaces[6] = {
            '_default': u'Image',
                'ar': u'صورة',
            'ca': u'Imatge',
            'da': u'Billede',
            'de': u'Bild',
            'el': u'Εικόνα',
            'es': u'Imagen',
            'fi': u'Kuva',
            'he': u'תמונה',
            'it': u'Immagine',
            'la': u'Imago',
            'no': u'Bilde',
            'pl': u'Grafika',
            'pt': u'Imagem',
            'ru': u'Изображение',
            'sv': u'Bild',
            'zh-tw': u'圖像',
        }

        self.namespaces[7] = {
            '_default': u'Image talk',
                'ar': u'نقاش الصورة',
            'ca': u'Imatge Discussió',
            'da': u'Billede diskussion',
            'de': u'Bild Diskussion',
            'el': u'Συζήτηση εικόνας',
            'es': u'Imagen Discusión',
            'fi': u'Keskustelu kuvasta',
            'fr': u'Discussion Image',
            'he': u'שיחת תמונה',
            'it': u'Discussioni immagine',
            'la': u'Disputatio Imaginis',
            'no': u'Bildediskusjon',
            'pl': u'Dyskusja grafiki',
            'pt': u'Imagem Discussão',
            'ru': u'Обсуждение изображения',
            'sv': u'Bilddiskussion',
            'zh-tw': u'圖像討論',
        }

            self.namespaces[8] = {
                '_default': u'MediaWiki',
                'ar': u'ميدياويكي',
                'he': u'מדיה ויקי',
            'zh-tw': u'媒體維基',
        }

            self.namespaces[9] = {
                '_default': u'MediaWiki talk',
                'ar': u'نقاش ميدياويكي',
            'ca': u'MediaWiki Discussió',
                'da': u'MediaWiki diskussion',
            'de': u'MediaWiki Diskussion',
            'es': u'MediaWiki Discusión',
            'fr': u'Discussion MediaWiki',
                'he': u'שיחת מדיה ויקי',
            'it': u'Discussioni MediaWiki',
            'la': u'Disputatio MediaWiki',
            'no': u'MediaWiki-diskusjon',
            'pl': u'Dyskusja MediaWiki',
                'pt': u'MediaWiki Discussão',
                'ru': u'Обсуждение MediaWiki',
            'sv': u'MediaWiki diskussion',
            'zh-tw': u'媒體維基討論',
        }

            #
            # Custom namespace list for en: (and fi:)
            #
            self.namespaces[100] = {
            '_default':u'Wilde',
            'en':u'Wilde',
            'fi':u'Hikiquote',
            'pl':u'Cytaty',
        }
            self.namespaces[101] = {
            '_default':u'Wilde talk',
            'en':u'Wilde talk',
            'fi':u'Hiktionary',
            'pl':u'Dyskucja cytatów',
        }
            self.namespaces[102] = {
            '_default':u'UnNews',
            'en':u'UnNews',
            'fi':u'Hikikirjasto',
            'pl':u'NonNews',
        }
            self.namespaces[103] = {'_default':u'UnNews talk'}
            self.namespaces[104] = {'_default':u'Undictionary'}
            self.namespaces[105] = {'_default':u'Undictionary talk'}
            self.namespaces[106] = {'_default':u'Game'}
            self.namespaces[107] = {'_default':u'Game talk'}
            self.namespaces[108] = {'_default':u'Babel'}
            self.namespaces[109] = {'_default':u'Babel talk'}
            self.namespaces[110] = {'_default':u'Forum'}
            self.namespaces[111] = {'_default':u'Forum talk'}

            # A few selected big languages for things that we do not want to loop over
            # all languages. This is only needed by the titletranslate.py module, so
            # if you carefully avoid the options, you could get away without these
            # for another wiki family.
            self.languages_by_size = ['en', 'pl', 'de', 'es', 'ru', 'fr']

        def hostname(self,code):
            return self.langs[code]

        def path(self, code):
            if code=='fi':
               return '/hikipedia/index.php'
            if code=='hu':
               return '/w/index.php'
            if code=='ja':
               return '/w/index.php'
            if code=='no':
               return '/index.php'
            if code=='pt':
               return '/w/index.php'
            if code=='sv':
               return '/w/index.php'
            if code=='zh-tw':
               return '/w/index.php'
            return '/wiki/index.php'

        def version(self, code):
            return "1.7"

Notas
-----

Idioma
~~~~~~

Para un sitio de lengua sola, la lengua especificado no importa mientras
es constante entre el usuario-config.py y families/foo\_family.py

La conexión falló. ¿Contraseña incorrecta?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Pywikipedia no devuelve más que el éxito, el fracaso, o recibe el error
de conexión. De ser posible, el intento que tiene acceso a los troncos
de servidor de web (apache usa access\_log por omisión) y mirar a las
cuerdas de URL. Asegúrese que su "path" es definido de manera apropiada
para su wiki en su archivo de familias:

.. code:: python

    def path (self, code):
           return '/wiki/index.php'

-  Mirar el `mozilla configuración <Example:Mozilla wiki>`__ para
   pistas.

La configuración desigual interwiki
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

En algunos proyectos (como Uncyclopedia), cada lengua funciona como wiki
independiente. Esto puede significar(pensar) que mesas interwiki se
diferencian de un wiki individual al otro dentro del mismo proyecto.
Interwiki.py es construido suponiendo que, si eslabones de interlenguaje
de salida estén disponibles en absoluto de una lengua, la lista de
lenguas de destinación de eslabón disponibles y la destinación URL para
cada uno hará juego perfectamente a través de todo el wikis en el
proyecto.

Esto conduce a algunas trampas potenciales:

-  Si una lengua omite la lengua de salida interwiki el apoyo
   completamente, hay que evitar dar una cuenta a pywikipediabot sobre
   esto wiki (en el usuario-config.py) para asegurar que hojas de
   interwiki.py que una lengua wiki intacto.

-  Si una lengua usa una mesa válida pero incompleta interwiki,
   controlando interwiki.py sobre aquella lengua wiki creará eslabones
   rotos. A diferencia del caso donde una lengua falla por todo el
   proyecto, no hay ningún workaround limpio y fácil.

-  Si una lengua en un proyecto ha sida bifurcado (no solamente(justo)
   reflejado), el interwiki para cada par de lengua individual indicará
   sólo uno de múltiples tenedores. Verifice el wiki su bot mira es el
   mismo que está siendo unido del wiki usted es editing - de otra
   manera el bot suprimirá algunos eslabones válidos como " la página no
   existe ".

Véase también
-------------

-  `Using the python
   wikibot <Special:MyLanguage/Manual:Pywikibot/Basic use>`__

.. raw:: mediawiki

   {{Languages|Manual:Pywikibot/Use on third-party wikis}}

Category:Pywikibot/es
