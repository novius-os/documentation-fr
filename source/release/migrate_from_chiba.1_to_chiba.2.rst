Guide de migration de la version Chiba 1 à la version Chiba 2
#############################################################


Mettre à jour son Novius OS et ses applications
***********************************************

Reportez-vous à la page :doc:`/install/upgrade` si vous ne l'avez pas encore fait.

Modification de vos développements
**********************************

Ruptures de compatibilité
-------------------------

.. _release/migrate_from_chiba.1_to_chiba.2/model_dataset:

Model : les colonnes d'un ``dataset`` sont encodées
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Si une colonne d'un ``dataset`` contient du HTML, vous devez ajouter un paramètre ``isSafeHtml`` pour ne pas qu'elle soit encodée.

.. code-block:: php
   :emphasize-lines: 8

    <?php
    return array(
        'data_mapping' => array(
            // ...
            'column_with_html' => array(
                'title' => 'Column with HTML',
                'column' => 'col_html',
                'isSafeHtml' => true,
            ),
            // ...
        ),
    );

.. seealso:: :ref:`Common configuration for Model <api:php/configuration/application/common>`

.. _release/migrate_from_chiba.1_to_chiba.2/crud_success:

CRUD : le callback ``success`` est appelée après le ``save``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dans le CRUD, à la mise à jour d'item, la fonction de callback ``success`` est appelée après le ``save`` (pas avant), comme pour la création.
Si vous utilisez ``success`` dans vos développements, vérifier que votre code soit compatible avec un appel après le ``save``.

.. _release/migrate_from_chiba.1_to_chiba.2/attachment:

Attachment : ``->url()`` et ``->urlResized()`` retournent des URL absolues
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Les méthodes ``->url()`` and ``->urlResized()`` retourne maintenant des URL absolues. Vous avez 2 possibilités de modification de vos développements :

* Vérifier que vous ne concateniez pas le ``base_url`` devant l'appel de ces méthodes.
* Ajouter un paramètre égal à ``false`` dans l'appel de la méthode.

    .. code-block:: php

        <?php

        $attachement->url(false);

.. seealso:: :ref:`api:php/classes/attachment`

.. _release/migrate_from_chiba.1_to_chiba.2/comments:

Comments : Les commentaires sont maintenant ``contextable``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

La migration essaye de deviner le contexte des commentaires existants, mais si vous avez implémenté les commentaires sur un modèle non ``contextable``,
la migration ne pourra rien. Dans ce cas vous devrez assigner vous-même les contexts aux commentaires
(colonne ``comm_context`` de la table ``nos_comment``) si vous voulez les voir dans l'interface d'administration.

.. _release/migrate_from_chiba.1_to_chiba.2/blognews:

Blog/News : La taille par défaut des vignettes change et elles sont cliquables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* La taille par défaut change de 200 à 120 pixels sur la liste, toujours 200 pour la fiche.
* Les vignettes sont cliquables.

Si vous voulez revenir à la configuration précédente :

* Étendez le fichier de configuration correspondant files :file:`noviusos_blog::config` ou :file:`noviusos_news::config`
* Modifier la configuration de cette façon :

    .. code-block:: php
	   :emphasize-lines: 7-8,11

        <?php

        return array(
            'thumbnail' => array(
                'front' => array(
                    'list' => array(
                        'link_to_item' => false,
                        'max_width' => 200.
                    ),
                    'item' => array(
                        'link_to_fullsize' => false,
                    ),
                ),
            ),
        );

Dépréciés
---------

Une mise en conformité n'est pas obligatoire mais souhaitable pour pouvoir migrer sans soucis lors de prochaine version.

.. _release/migrate_from_chiba.1_to_chiba.2/enhancer:

Enhancer : ``get_url_model($item, $params)`` devient ``getURLEnhanced($params)``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Code déprécié :

.. code-block:: php

    <?php

    public static function get_url_model($item, $params = array())
    {
        $model = get_class($item);

        switch ($model) {
            case 'A\Class':
                return $item->virtual_name).'.html';
                break;
        }

        return false;
    }

À remplacer par :

.. code-block:: php

    <?php

    public static function getURLEnhanced($params = array())
    {
        $item = \Arr::get($params, 'item', false);
        if ($item) {
            $model = get_class($item);

            switch ($model) {
                case 'A\Class':
                    return $item->virtual_name).'.html';
                    break;
            }
        }

        return false;
    }

.. _release/migrate_from_chiba.1_to_chiba.2/media:

Media : Changement dans l'API de Model_Media
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Toutes les méthodes en ``snake_case`` sont dépreciées :

* ``delete_from_disk`` devient ``deleteFromDisk``
* ``delete_public_cache`` devient ``deleteCache``
* ``get_path`` devient ``_getVirtualPath``
* ``get_private_path`` devient ``path``
* ``get_img_tag`` devient ``htmlImg``
* ``get_img_tag_resized`` devient ``htmlImgResized``
* ``is_image`` devient ``isImage``
* ``get_public_path`` devient ``url``
* ``get_public_path_resized`` devient ``urlResized``

.. seealso:: :ref:`api:php/models/media/model_media/methods`

.. _release/migrate_from_chiba.1_to_chiba.2/media_folder:

Media : Changement dans l'API de Model_Folder
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``delete_from_disk`` devient ``deleteFromDisk``
* ``delete_public_cache`` devient ``deleteCache``

.. seealso:: :ref:`api:php/models/media/model_folder/methods`

.. _release/migrate_from_chiba.1_to_chiba.2/page_link:

Page : Model_Page->link() dépréciée
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``Model_Page->link()`` est déprécié, utiliser ``Model_Page->htmlAnchor()``.

.. warning::

    ``Model_Page->link()`` ne retournait que les attributs ``href`` et ``target``, ``Model_Page->htmlAnchor()``
    retourne le tag HTML ``<a>`` en entier.

.. seealso:: :ref:`api:php/models/model_page/methods`

.. _release/migrate_from_chiba.1_to_chiba.2/user_login:

L'événement ``user_login``
^^^^^^^^^^^^^^^^^^^^^^^^^^

L'événement ``user_login`` est déprécié, utiliser ``admin.loginSuccess`` à la place.

.. seealso:: :ref:`api:php/events/admin.loginSuccess`

