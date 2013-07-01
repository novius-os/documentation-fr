Créer votre Behaviour
#####################


Vous pouvez ajouter n'importe quelle classe en tant que Behaviour en ajoutant son nom de classe complet dans la
propriété ``$_behaviours`` de votre modèle.


Étendre la classe Orm_Behaviour
===============================

Pour créer un behaviour, il faut créer une classe qui étend **Nos\\Orm_Behaviour**, ainsi que les méthodes d'évènements
sur lesquels vous voulez  que votre Behaviour agisse.


Properties
----------

Lors de leur définition, les behaviours peuvent avoir un tableau de configuration, qui sera disponible dans la variable
**$this->_properties** à l'intérieur du behaviour.

.. code-block:: php

    <?php

    class Model_Monkey extends Nos\Orm\Model
    {
        protected static $_behaviours = array(
            'My_Behaviour' => array(
                'configuration' => 'defined here',
            ),
        );
    }

.. code-block:: php

    <?php

    class My_Behaviour extends Nos\Behaviour
    {
        /*
         * Dans n'importe quelle méthode, $this->_properties aura la valeur :
         * array(
         *     'configuration' => 'defined here',
         * )
         */
    }


Ensuite, il faut y ajouter quelques évènements, qui sont de deux types : ceux **d'instance** et ceux **statiques**.


Les évènements d'instance
-------------------------

Les évènements d'instance agissent en fonction d'une instance d'un modèle. Ils reçoivent systématiquement cette dernière
en tant que premier paramètre, plus éventuellement d'autres paramètres spécifiques à l'évènement.

La :ref:`liste des évènements d'instance <api:php/behaviours/behaviour_event/instance>` est disponible dans la documentation d'API.

Exemple avec l'évènement d'instance **form_processing** (déclenché lors de la sauvegarde d'un item via le CRUD).

.. code-block:: php

    <?php

    class My_Behaviour extends Nos\Behaviour
    {
        public function form_processing(Nos\Orm\Model $item, $data, &$json_repsonse)
        {
            // Exemples :
            // On remplit des valeurs à sauvegarder dans l'item
            // On rajoute une clé dans le tableau JSON
        }
    }

    // Pour information : en interne, Novius OS fait appel à cet évènement via ce code suivant :
    $item->event('form_processing', array($data, &$json_response));


L'évènement sera appelé pour tous les Behaviour qui ont implémenté la méthode correspondante.


Les évènements statiques
------------------------

Les évènements statiques agissent de manière générale sur un modèle, et non pas sur une instance particulière de ce dernier.

La :ref:`liste des évènements statiques <api:php/behaviours/behaviour_event/static>` est disponible dans la documentation d'API.

Les méthodes statiques ne reçoivent pas l'instance du modèle en tant que premier paramètre, mais uniquement les paramètres
spécifiques à l'évènement.

Par exemple, les behaviours peuvent écouter des évènements qui leur permettent de modifier la configuration de l'AppDesk ou du CRUD.

On citera :

- Le behaviour :ref:`Publishable <api:php/behaviours/publishable>`, qui rajoute un champ dans la configuration du CRUD et
  qui l'affiche en utilisant le Renderer_Publishable.
- les behaviours :ref:`Urlenhancer <api:php/behaviours/urlenhancer>`, :ref:`Twinnable <php/behaviours/twinnable>` et :ref:`Sharable <php/behaviours/sharable>`
  qui rajoutent respectivement les actions **visualiser**, **traduire** et **partager**.

Exemple avec l'évènement **crudConfig** :

.. code-block:: php

    <?php

    class My_Behaviour extends Nos\Behaviour
    {
        public function crudConfig(&$config, $controller)
        {
            // Exemples :
            // On rajoute un champ en modifiant $config['fields']
        }
    }

    // Pour information : en interne, Novius OS fait appel à cet évènement via ce code suivant :
    Model_Class::eventStatic($config, $controller);
