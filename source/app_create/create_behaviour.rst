Créer votre Behaviour
#####################


À quoi ça sert ?
================

Créer un behaviour permet d'appliquer un même comportement sur plusieurs modèles différents, en partageant la même
base de code réutilisable.

Les behaviours sont une extension du mécanisme d'observers présents dans FuelPHP. Ils permettent notamment (comme pour
les observers), d'écouter les notifications ``before_*`` et ``after_*`` déclenchées par FuelPHP.

Les behaviours permettent deux fonctionnalités supplémentaires :

* d'écouter des évènements déclenchés par Novius OS (notamment par le CRUD et l'AppDesk) ;
* d'ajouter dynamiquement des méthodes supplémentaires sur vos modèles (et de manière réutilisable).

Voici quelques exemples pour illustrer ces propos :

* ajout d'une action dans l'App Desk ou le CRUD ;
* ajout d'une colonne dans le dataset (data_mapping) d'un modèle ;
* ajout d'un champ dans le formulaire d'ajout / d'édition d'un item ;
* ajout d'une méthode 'myBehaviourMethod()' pour tous les modèles utilisant ce behaviour.

On citera :

- Le behaviour :ref:`Publishable <api:php/behaviours/publishable>`, qui rajoute un champ dans la configuration du CRUD et
  qui l'affiche en utilisant le Renderer_Publishable.
- Les behaviours :ref:`Urlenhancer <api:php/behaviours/urlenhancer>`, :ref:`Twinnable <php/behaviours/twinnable>` et :ref:`Sharable <php/behaviours/sharable>`
  qui rajoutent respectivement les actions **visualiser**, **traduire** et **partager**.



Étendre la classe Orm_Behaviour
===============================

Pour créer un behaviour, il faut créer une classe qui étend **Nos\\Orm_Behaviour**, puis implémenter :

* les méthodes d'évènements déclenchés par FuelPHP (``before_*`` et ``after_*``), de la même manière que pour les Observer ;
* les méthodes d'évènements déclenchés par Novius OS (notamment par le CRUD et l'AppDesk) ;
* les méthodes que vous voulez rendre disponibles sur les modèles qui utilise votre behaviour.


Vous pouvez ajouter n'importe quelle classe en tant que Behaviour en ajoutant son nom de classe complet dans la
propriété ``$_behaviours`` de votre modèle.


Properties
----------

Comme avec un observer FuelPHP, les modèles peuvent spécifier un tableau de configuration dans leur définition des
behaviours. Cette configuration sera disponible dans la variable **$this->_properties** à l'intérieur du behaviour.

.. code-block:: php

    <?php

    class Model_Monkey extends Nos\Orm\Model
    {
        protected static $_behaviours = array(
            'My_Behaviour' => array(
                'my_key' => 'my_value',
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
         *     'my_key' => 'my_value',
         * )
         */
    }


Écouter un évènement déclenché par FuelPHP (Observer)
-----------------------------------------------------

Ce sont les évènements de type ``before_*`` et ``after_*``.

Par exemple, ``Behaviour_Author`` stocke l'ID des utilisateurs ayant créé / modifié un item dans une colonne du modèle grâce
(respectivement) aux évènements ``before_insert`` et ``before_save`` `fournis par l'ORM de FuelPHP <http://fuelphp.com/docs/packages/orm/observers/creating.html#/event_names>`__.


.. code-block:: php

    <?php

    class Orm_Behaviour_Author extends Orm_Behaviour
    {
        public function before_insert(\Nos\Orm\Model $item)
        {
            $created_by_property = \Arr::get($this->_properties, 'created_by_property', null);
            if ($created_by_property === null) {
                return;
            }

            $user = \Session::user();
            if (!empty($user)) {
                $item->{$created_by_property} = $user->user_id;
            }
        }
    }


Écouter un évènement déclenché par Novius OS
--------------------------------------------

De la même manière que pour les observers, il faut implémenter une méthode qui porte le même nom de l'évènement déclenché.

Par exemple, pour écouter l'évènement **form_processing**, on implémentera la méthode **form_processing()**.

La différence avec les évènements déclenchés par FuelPHP réside dans les paramètres envoyées à ces méthodes :

Là où les méthodes d'Observer (``before_*`` et ``after_*``) prennent un unique paramètre **$item** (instance du modèle),
les évènements déclenchés par Novius OS peuvent en prendre plusieurs, et dépendent du type d'évènement.

Il existe deux types d'évènements :

* les évènements d'instance, qui prennent systématiquement l'**$item** en premier paramètre, plus éventuellement d'autres paramètres spécifiques à l'évènement ;
* les évènements statiques, qui reçoivent uniquement les paramètres spécifiques à l'évènement.

La :ref:`liste des évènements (d'instance et statiques) <api:php/behaviours/behaviour_event>` est disponible dans la documentation d'API.

Un évènement est appelé sur tous les Behaviour qui ont implémenté la méthode correspondante. La valeur de retour de ces méthodes
n'a pas d'importance : les évènements utilisent les `arguments passés par référence <http://php.net/manual/fr/language.references.pass.php>`__
pour agir.


Exemple avec l'**évènement d'instance** ``form_processing`` (déclenché lors de la sauvegarde d'un item via le CRUD).

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


Exemple avec l'**évènement statique** ``crudConfig``

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
    Model_Class::eventStatic('crudConfig', $config, $controller);


Rajouter dynamiquement une méthode d'instance sur un modèle
-----------------------------------------------------------

De la même manière que les évènements déclenchés par FuelPHP et les évènements d'instance, les méthodes dynamiques portent
le même nom que la méthode à rajouter sur le modèle et prennent en premier paramètre **$item**, l'instance du modèle.

Contrairement aux évènements, une méthode retourne généralement une valeur.

Par exemple, le ``Behaviour_Contextable`` dans Novius OS rajoute la méthode ``get_context()`` sur les modèles qui l'utilisent :

.. code-block:: php

    <?php

    // Model file
    class Model_Monkey extends Nos\Orm\Model
    {
        protected static $_behaviours = array(
            'Orm_Behaviour_Contextable' => array(
                'context_property' => 'monk_context',
            ),
        );
    }


    // Behaviour file
    class Orm_Behaviour_Contextable extends Nos\Behaviour
    {
        public function get_context(Orm\Model $item)
        {
            return $item->get($this->_properties['context_property']);
        }
    }

    // Use case
    $monkey = Model_Monkey::find('first');

    // Cette méthode est disponible parce que Model_Monkey utilise Behaviour_Contextable, qui la rajoute
    $context = $monkey->get_context();


Rajouter dynamiquement une méthode statique sur un modèle
---------------------------------------------------------

De la même façon que pour une méthode d'instance mais plus besoin du premier paramètre **$item**.

.. code-block:: php

    <?php

    // Model file
    class Model_Monkey extends Nos\Orm\Model
    {
        protected static $_behaviours = array(
            'Orm_Behaviour_Twinnable' => array(
                'context_property'      => 'monk_context',
                'common_id_property' => 'monk_context_common_id',
                'is_main_property' => 'monk_context_is_main',
                'common_fields'   => array('monk_species_common_id', 'monk_birth_year'),
            ),
        );
    }


    // Behaviour file
    class Orm_Behaviour_Twinnable extends Nos\Behaviour
    {
        public function hasCommonFields()
        {
            $class = $this->_class;
            return count($this->_properties['common_fields']) > 0 ||
                static::sharedWysiwygsContext($class) > 0 ||
                static::sharedMediaContext($class) > 0;
        }
    }

    // Use case
    Model_Monkey::hasCommonFields();

