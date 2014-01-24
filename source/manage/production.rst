Mise en production
##################

Transfert de l'instance sur le serveur de production
****************************************************

Il y a plusieurs façons d'envoyer une instance Novius OS sur votre serveur de production :

* La façon la plus simple serait de copier tous les fichiers de l'instance ainsi que la base de donnée sur le serveur.
  Cependant, comme les données sont généralement différentes entre ces deux instances, ce n'est pas très pratique. Et
  vous aurez probablement à modifier les fichiers de configuration.
* Vous pouvez envoyer tous les fichiers sauf ceux des dossiers `local/metadata` et `local/data`. Vous devrez installer
  Novius OS sur le serveur la première fois. Ainsi, la configuration de mysql, des urls, et du compte administrateur se
  fera facilement.

Cependant, quelque soit la méthode que vous choisissez, vous devrez changer quelques éléments de configurations afin
d'améliorer l'optimisation.

Changer l'environnement en mode production
******************************************

La première étape est de changer l'environnement Fuel (enregistré sous `Fuel::$env`). Cela adaptera automatiquement
quelques paramètres tels que la durée de vie du cache ou le niveau des logs. Le
`site de FuelPHP <http://fuelphp.com/docs/general/environments.html#/env_apache>`__ explique comment changer cet
environnement.

Vous pouvez le faire en changeant le valeur de `SetEnv` dans la configuration d'Apache.

.. code-block:: apacheconf

    SetEnv FUEL_ENV production
    // ou
    SetEnv NOS_ENV production

Configuration de connection à la base de données
************************************************

Vous devez ajouter la clé `production` dans le fichier de configuration `local/config/db.config.php`. La configuration
peut être assez similaire que celle de la clé `development`; si vous avez installé votre instance directement sur le
serveur de production, vous n'avez juste qu'à renommer la clé `development` en `production`. Le
`site de FuelPHP <http://fuelphp.com/docs/classes/database/introduction.html>`__ documente très bien comment configurer
l'accès à votre base de données.

Modifier les durées de vie du cache
***********************************

La durée de vie du cache est adaptée si l'environnement est en production. Vous pouvez néanmoins la changer en
modifiant le fichier `local/config/config.php`.

.. code-block:: php

    return array(
        'novius-os' => array(
            'cache' => true,
             // Les durées de vie de cache sont par défaut à 3600 secondes en mode production
            'cache_duration_page' => 3600, // durée de vie du cache des pages
            'cache_duration_function' => 3600, // durée de vie du cache des autres éléments (applications...)
            'cache_model_properties' => false, // définit si Novius OS enregistrer les propriété des modèles dans le
            // cache. S'applique uniquement aux modèles dont les propriétés ne sont pas définies
        ),
    );

Configuration des emails
************************

Si vous avez besoin que votre instance Novius OS puisse envoyer des emails, vous devez renommer votre fichier
`local/config/email.config.php.sample` en `local/config/email.config.php`. Les détails de configuration sont très bien
expliqués dans le `site de FuelPHP <http://fuelphp.com/docs/packages/email/introduction.html>`__.