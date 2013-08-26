Les bases de FuelPHP
====================

Qu'est-ce que le MVC ?
----------------------

C'est l'acronyme de Modèle-Vue-Contrôleur.

C'est une approche pour séparer votre code en fonction du rôle qu'il joue. De manière simplifiée, une requête est traitée
par un **contrôleur**. Ce dernier charge des données en passant par les **modèles**. Enfin, il décide quelle **vue** sera
utilisée pour afficher les données qui seront visibles par vos visiteurs.

.. seealso:: `MVC dans la documentation FuelPHP <http://fuelphp.com/docs/general/mvc.html>`__

.. seealso:: `MVC dans Wikipedia <http://fr.wikipedia.org/wiki/Modèle-Vue-Contrôleur>`__


Où créer mes nouveaux fichiers ?
--------------------------------

Toutes les classes respectent la même convention de nommage précise :

* en minuscule, sauf la première lettre de chaque niveau en majuscule ;
* les underscore jouent le rôle de dossier.

Par exemple le fichier :file:`classes/controller/admin/login.php` correspond à la classe nommée ``Controller_Admin_Login``.

Les `classes <http://fuelphp.com/docs/general/classes.html>`__ PHP se situent dans le dossier :file:`classes`.

Les classes `contrôleurs <http://fuelphp.com/docs/general/controllers/base.html>`__ trouvent leur place dans le dossier :file:`classes/controller`.

Les classes `modèles <http://fuelphp.com/docs/general/models.html>`__ vont dans :file:`classes/model`.


Comment écrire une vue ?
------------------------

Les vues sont situées dans le dossier :file:`views`.


.. seealso:: `Documentation de FuelPHP sur les vues <http://fuelphp.com/docs/general/views.html>`__



Comment utiliser l'ORM ?
------------------------

Un ORM permet 2 choses :

* accéder à vos données en base sous forme d'objets PHP ;
* établir des relations entre ces objets.

L'ORM de FuelPHP utilise le pattern `Active Record <http://fr.wikipedia.org/wiki/Active_record_(patron_de_conception)>`__.

Les liens suivants vers la documentation de FuelPHP vous seront utiles :

.. seealso:: `Créer des modèles <http://fuelphp.com/docs/packages/orm/creating_models.html>`__

.. seealso:: `Faire des requêtes à partir des modèles <http://fuelphp.com/docs/packages/orm/creating_models.html>`__

.. seealso:: `Définir des relations et s'en servir dans les requêtes <http://fuelphp.com/docs/packages/orm/relations/intro.html>`__



