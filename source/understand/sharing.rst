Partage de contenu
******************

.. seealso::

	`Infographie « Partage dans Novius OS » <http://novius-os.github.com/docs/fr/applications.html#sharing>`__


.. _sharing_content-nuggets:

Content nuggets
===============

Un « content nugget », ou pépite de contenu, est un ensemble cohérent de données destiné à être partagé.

Structure des données
---------------------

Les données d'un content nugget peuvent être de la nature suivante :

* Titre
* URL
* Texte
* Image

Pour qu’une application puisse partager son contenu, il suffit de lui assigner le :ref:`Behaviour Sharable <api:php/behaviours/sharable>` et définir quelles sont les données constituant le content nugget.


.. _sharing_data-catchers:

Data catchers
=============

Les data catchers sont des composants d’une application qui exploitent les content nuggets (eux-mêmes générés par les modèles).

Ils sont définis dans le fichier :file:`metadata.config.php` d’une application, à l’image des autres composants (gabarits, enhancers et launchers).

Data catchers inclus dans le logiciel
-------------------------------------

* Simple Twitter
* Simple Facebook
* Simple Google+
* Blog

Le data catcher ``Blog`` est utilisé pour créer des billets de blog à partir du contenu d’autres applications, notamment d’applications métiers spécifiques. Vous ajoutez, par exemple, un nouveau produit à votre catalogue, vous préparez facilement un billet de blog annonçant cette nouveauté.


Exemple : Simple Twitter
------------------------

Voici comment est défini le data catcher de partage simple vers Twitter :

.. code-block:: php

	<?php

	return array(
        'data_catchers' => array(
            'noviusos_simpletwitter' => array(
                'title' => 'Twitter',
                'description'  => '',
                'iconUrl' => 'static/apps/noviusos_simpletwitter/img/twitter.png',
                'action' => array(
                    'action' => 'window.open',
                    'url' => 'https://twitter.com/intent/tweet?text={{urlencode:'.\Nos\DataCatcher::TYPE_TITLE.'}}&url={{urlencode:absolute_url}}',
                ),
                'onDemand' => true,
                'specified_models' => false,
                'required_data' => array(
                    \Nos\DataCatcher::TYPE_TITLE,
                ),
                'optional_data' => array(
                    \Nos\DataCatcher::TYPE_URL,
                ),
            ),
        ),
	);

Le data catcher **Simple Twitter** exploite des content nuggets ayant au moins un titre. L'URL est optionnelle, mais est utilisée quand elle est fournie.
