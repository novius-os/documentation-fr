Notes de la version Elche
#########################

Nouveautés
==========

* Nouvelle application **Menu** pour gérer les menus de son site web.
* Nouvelle application **Déclinaison de gabarit** pour gérer des déclinaisons de gabarit par contexte.
* Nouvelle application **Gabarit Bootstrap personnalisable** qui utilise les déclinaisons de gabarit. Vous pouvez personnaliser les elements, la mise en page, le thème, les menus.
* **UI**: L'image de fond est sur le ``body`` et ses bords sont visibles en permanence
* **UI**: Nouvelle barre système avec une nouvelle fonctionnalité plein écran
* **UI**: La barre d'outils des Appdesks et CRUDs est en bas
* **UI**: Sur le bureau, les applications sont maintenant organisable sur une grille, et non plus juste triable
* **Renderer**: Nouveau renderer ``Renderer_Item_Picker`` basé sur l'appdesk natif de modèle
* **Renderer**: Nouveau renderer ``Renderer_Select_Model`` pour sélectionner un item d'un modèle. Gère les comportement contexable et twinnable.

Développeur
===========

* **ORM**: Ajout d'un système de Providers. Possibilité d'ajouter des providers à un modèle. Les providers sont des assecceurs par clé d'items liés par relation.
* **ORM**: Les Wysiwygs et Medias deviennent des providers natifs.
* **ORM**: Nouveau providers ``shared_wysiwygs_context`` et ``shared_medias_context``.
* **Enhancer**: La configuration de popup gère la validation de formulaire si des champs ont des contraintes.
* **Grid**: Les ``cellFormatters`` sur les colonnes fonctionnent sur tous les widgets ``noslistgrid``, plus seulement sur le tableau principal de l'appdesk

Ruptures de compatibilité
-------------------------

* :ref:`release/migrate_from_dubrovka_to_elche/shared_wysiwygs_medias`

Mise à jour des librairies tierces
----------------------------------

* jQuery 1.11.1
* jQuery UI 1.10.4
* Wijmo 2014v1.34
* require.js 2.1.11
* pNotify 2.0
* JQuery.cookie 1.4.1
* JQuery.form 3.50.0-2014.0.2.05
* JQuery.mousewheel 3.1.11
* JQuery.datetimepicker 1.4.4
* Webshims 1.13, in Form application,

Dépréciés
---------

* :ref:`release/migrate_from_dubrovka_to_elche/nos_methods`
