Guide de migration de la version Chiba 2 à la version Dubrovka
##############################################################

Mettre à jour son Novius OS et ses applications
***********************************************

Reportez-vous à la page :doc:`/install/upgrade` si vous ne l'avez pas encore fait.

Modification de vos développements
**********************************

Ruptures de compatibilité
-------------------------

.. _release/migrate_from_chiba.2_to_d/fuelphp:

FuelPHP de la 1.6 à la 1.7.1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Jetez un oeil à ces trois changelog de ​​FuelPHP pour lesnotes de compatibilité ascendante :

* `FuelPHP 1.6.1 <https://github.com/fuel/fuel/blob/f5c031a32e2e205eec573121d8417360cef4d609/CHANGELOG.md>`__
* `FuelPHP 1.7 <https://github.com/fuel/fuel/blob/1c4e81b3941c833a8dcf0e6565d4bbe68dc65f03/CHANGELOG.md>`__
* `FuelPHP 1.7.1 <https://github.com/fuel/fuel/blob/8bdfa36e2173ed2afeb28455760cf4bfe68f96ff/CHANGELOG.md>`__

.. _release/migrate_from_chiba.2_to_d/wijmo:

Wijmo de la 2013v1.4 à la 2013v3.20
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Jetez un oeil aux notes de version de Wijmo entre 2013v3.20 et 2013v1.4: http://wijmo.com/wiki/index.php/Version_Histories

.. _release/migrate_from_chiba.2_to_d/migrations.enabled_types.metadata:

Fin de support pour la clé de key migrations.enabled_types.metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

La clé de config ``migrations.enabled_types.metadata`` n'est plus supportée,
et la méthode ``Migration::canUpdateMetadata()`` n'existe plus.
Durant les migrations, tous les fichiers de :file:`local/metadata` sont supposés être inscriptible.

Un nouveau événement :ref:`migrate.exception <api:php/events/migrate.exception>` est déclenché si une migration génère une exception.
Cet évenement peut arrêter la propagation de l'exception.

Dépréciés
---------

Une mise en conformité n'est pas obligatoire mais souhaitable pour pouvoir migrer sans soucis lors de prochaine version.

.. _release/migrate_from_chiba.2_to_d/i18n_crud_config:

Des clés i18n de la config du CRUD pour les formes plurielles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Le système de traduction de Novius OS respectte maintenant les formes plurielles des langues. Quelques clés i18n de la configuration du CRUD sont affectées.

Ces clés doivent maintenant contenir un tableau des différents pluriels traduits, et plus le texte traduit :

* ``deleting with N contexts``
* ``deleting with N languages``
* ``deleting with N children``
* ``deleting button N items``
* ``N items``
* ``showNbItems``

Ces clés ne sont plus utiles :

* ``1 child``
* ``deleting button 1 item``
* ``deleting button 0 items``
* ``1 item``


.. _release/migrate_from_chiba.2_to_d/hmvc:

L'API de Nos::hmvc() est simplifiée
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Le second argument peut être juste un tableau et lpus un tableau avec une clé ``args`` contenant un tableau.

Code déprécié :

.. code-block:: php

    <?php

    \Nos::hmvc('request/url/', array('args' => array($first_parameter, $second_parameter)));

À remplacer par :

.. code-block:: php

    <?php

    \Nos::hmvc('request/url/', array($first_parameter, $second_parameter));

.. _release/migrate_from_chiba.2_to_d/loadConfiguration:

Méthode \Config::loadConfiguration()
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

La méthode ``\Config::loadConfiguration()``. Utiliser ``\Config::load()``.

Code déprécié :

.. code-block:: php

    <?php

    $config = \Config::loadConfiguration('application_name', 'file_name');
    //or
    $config = \Config::loadConfiguration('application_name::file_name');

À remplacer par :

.. code-block:: php

    <?php

    $config = \Config::load('application_name::file_name', true);

.. _release/migrate_from_chiba.2_to_d/applicationRequiredFromMetadata:

La portée publique de \Nos\Application::applicationRequiredFromMetadata()
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

La méthode ``\Nos\Application::applicationRequiredFromMetadata()`` n'est pas censé être appellée à l'extérieur de la classe ``\Nos\Application``.
Elle deviendra ``protected`` dans le futur.

Vous pouvez avoir la liste des dépendances des applications en chargeant le fichier metadata :file:`app_dependencies`.

.. code-block:: php

    <?php

    $dependencies = \Nos\Config_Data::get('app_dependencies', array());

.. _release/migrate_from_chiba.2_to_d/extends.application:

Dans les fichiers metadata, la clé ``extends.application``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dans les fichiers metadata, la syntaxe de la clé ``extends`` contenant un tableau avec une clé ``application`` est dépréciée.

La clé ``extends`` doit contenir juste un tableau avec le nom des applications étendues en valeurs.

Code déprécié :

.. code-block:: php

    <?php

    return array(
        'name'    => 'Application name',
        //...
        'extends' => array(
            'application' => 'application_name',
            'extend_configuration' => false,
        ),
    );

À remplacer par :

.. code-block:: php

    <?php

    return array(
        'name'    => 'Application name',
        //...
        'extends' => array(
            'application_name',
        ),
    );

.. _release/migrate_from_chiba.2_to_d/extends.apps:

Les fichiers de config étendus par une application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Les fichiers de config étendus par une application doivent être définis dans un sous-répertoire :file:`apps/application_name/`

Par exemple, si votre application A étend le fichier exemple.config.php de l'application B.

Emplacement déprécié : :file:`local/applications/application_a/config/exemple.config.php`

Le déplacer vers : :file:`local/applications/application_a/config/apps/application_b/exemple.config.php`


.. _release/migrate_from_chiba.2_to_d/wysiwyg_theme:

WYSIWYG theme
^^^^^^^^^^^^^

L'utilisation du theme ``advanced`` est déprécié, utiliser exclusivement le thème ``nos``.

Le thème ``nos`` est maintenant une extension du thème ``advanced``.
Toutes les clés de configuration commençant par ``theme_nos_`` sont dépréciées et doivent être remplacées par leur équivalent commençant par ``theme_advanced_``.