Avoir des champs commun à tous les contextes
############################################

Si votre application est ``Twinnable``, vous voulez peut-être rendre certains champs d'un modèle commun à tous les contextes.
Par exemple, dans l'application ``Monkey`` l'année de naissance, l'espèce et la photo d'un singe ne sont pas dépendantes du contexte.
Un singe en version française aura la même année de naissance, la même espèce et la même photo que dans sa version anglaise.

.. seealso:: :doc:`/understand/multi_context/index`

Champ commun
************

Pour définir un champ commun à tous les contextes pour un model, il suffit de le déclarer dans la clé ``common_fields`` du comportement ``Twinnable``.

Exemple
*******

.. code-block:: php

    <?php
    class Model_Page extends \Nos\Orm\Model
    {
        protected static $_behaviours = array(
            'Nos\Orm_Behaviour_Twinnable' => array(
                'context_property'      => 'monk_context',
                'common_id_property' => 'monk_context_common_id',
                'is_main_property' => 'monk_context_is_main',
                'common_fields'   => array('monk_species_common_id', 'monk_birth_year'),
            ),
        );
    }

Média et WYSIWYG commun
***********************

Pour définir un média ou un WYSIWYG commun à tous les contextes pour un model, il suffit d'utiliser
les :ref:`providers <api:php/behaviours/twinnable/providers>` ``shared_wysiwygs_context`` et ``shared_medias_context`` ajoutés par le comportement ``Twinnable``.
