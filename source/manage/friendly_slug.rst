Formatage des URL
#################

Tous les segments d'URL construient dans Novius OS sont formattés avec le mécanisme "friendly slug".

Par défaut :

    * Les caractères ``?``, ``:``, ``\``, ``/``, ``#``, ``[``, ``]``, ``@``, ``&`` et l'espace sont remplacés par un ``-``.
    * Transformation en minuscules.
    * Suppression des ``-`` en début ou fin de chaine.
    * Remplacement de ``-`` consécutifs par un seul.

Mais vous pouvez utiliser d'autres règles ou définir vos propres règles.
Vous pouvez également avoir des règles spéciales pour les :doc:`contextes </understand/multi_context/principles>`.

Quatre lots de règles sont définis :

* ``default`` (comme décrit ci-dessus)
* ``no_accent``. Tous les accents sont remplacés par un caractère équivalent non accentué.
* ``no_special``. Tous les caractères qui ne sont pas des caractères de mot, le ``-`` ou le ``_`` sont remplacés par ``-``.
* ``no_accent_and_special``. Combinaison des lots de règles ``no_accent`` et ``no_special``.

Un fichier de configuration d'exemple est disponible : :file:`local/config/friendly_slug.config.php.sample`.
Si vous voulez modifier les règles appliquées par défaut, renommez ou copiez le fichier en :file:`local/config/friendly_slug.config.php`,
et modifiez le selon votre cas.

Règles par défaut
=================

Pour changer les règles par défaut :

* créez un jeu de règle dans ``setups``.
* Définissez l'``active_setup`` égal à ce jeu.

.. code-block:: php

    <?php
    return array(
        'active_setup' => 'my_default',

        'setups' => array(
            'my_default' => array(
                // Utilise les règles 'no_accent'
                'no_accent',

                // Remplace l'espace en '_'
                ' ' => '_',

                 // Tous les caractères qui ne sont pas des mots, un '-' ou un '_' ou un '*' sont remplacés par '-'.
                '[^\w\*\-_]' => array('replacement' => '-', 'flags' => 'i'),
            ),
        ),
    );

Règles par contexte
===================

Pour définir des règles spécifiques à un contexte, définir une clé avec l'ID de contexte dans le tableau ``setups``.

.. code-block:: php

    <?php
    return array(
        'setups' => array(
            'main::en_GB' => array(
                //... Définissez ici vos règles spécifiques au contexte main::en_GB
            ),
        ),
    );


.. seealso::

	:ref:`Documentation API sur le "Friendly slug" <api:php/configuration/friendly_slug>`.