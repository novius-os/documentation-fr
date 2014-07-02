Guide de migration de la version Dubrovka à la version Elche
############################################################

Mettre à jour son Novius OS et ses applications
***********************************************

Reportez-vous à la page :doc:`/install/upgrade` si vous ne l'avez pas encore fait.

Modification de vos développements
**********************************

Ruptures de compatibilité
-------------------------

.. _release/migrate_from_dubrovka_to_elche/shared_wysiwygs_medias:

Média et WYSIWYG commun aux contextes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Tous les Wysiwygs et Medias communs doivent être appellés avec les providers ``shared_wysiwygs_context`` et ``shared_medias_context``
* Enlever les déclaration des variables ``shared_wysiwygs_context`` et ``shared_medias_context`` des modèles.

Dépréciés
---------

Une mise en conformité n'est pas obligatoire mais souhaitable pour pouvoir migrer sans soucis lors de prochaine version.

.. _release/migrate_from_dubrovka_to_elche/nos_methods:

Nos:parse_wysiwyg(), Nos:parse_enhancers() et Nos:get_enhancer_content()
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ces méthodes sont dépréciées, utilisez :

* ``Tools_Wysiwyg::parse()`` à la place de ``Nos:parse_wysiwyg()``
* ``Tools_Wysiwyg::parseEnhancers()`` à la place de ``Nos:parse_enhancers()``
* ``Tools_Enhancer::content()`` à la place de ``Nos:get_enhancer_content()``
