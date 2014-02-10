Notes de la version Dubrovka
############################

Nouveautés
==========

* Les applications peuvent étendre plusieurs applications
* Le mécanisme d'extension d'application fonctionne aussi pour les vues et les fichiers de traductions, plus seulement pour les fichiers de configuration
* Traductions Russe
* Traductions Espagnol
* Traductions Interlingue (Occidental)
* Traductions Japonaise mise à jour

Développeur
===========

Ruptures de compatibilité
-------------------------

* :ref:`release/migrate_from_chiba.2_to_d/fuelphp`
* :ref:`release/migrate_from_chiba.2_to_d/wijmo`
* :ref:`release/migrate_from_chiba.2_to_d/migrations.enabled_types.metadata`

Mise à jour des librairies tierces
----------------------------------

* FuelPHP 1.7.1
* Wijmo 2013v3.20
* jQuery 1.10.2
* require.js 2.1.9
* TinyMCE 3.5.10
* JQuery.cookie 1.4
* JQuery.form 3.46.0-2013.11.21
* JQuery.validation 1.11.1
* JQuery.mousewheel 3.1.6
* JQuery.datetimepicker 1.4.3

Améliorations
-------------

* **UI** Intégration du nouveau logo Novius OS
* **UI**: L'affichage est amélioré quand on change d'onglet avant la fin de son chargement
* **Installation**: Amélioration des messages dans la première étape de l'assistant de paramétrage pour faciliter la compréhension des potentiels problèmes
* **i18n**: Ajout du méchanisme des pluriels et implémentation de traduction avec pluriels
* **Renderer**: Le selecteur de pages peut maintenant sélectionner plusieurs pages en utilisant des checkboxes
* **Renderer**: Ajout d'une méthode générique ``Renderer::renderer()`` pour tous les renderers qui étendent ``Renderer``
* **WYSIWYG**: Refactorisation des fonctionnalités TinyMCE propre à Novius OS. Toutes les fonctionnalités sont éclatées en plugins, beaucoup plus modulaire.
* **404**: Possibilité d'utiliser l'application ``novius_ftplite`` pour fournir des fichier ``robots.txt`` personnalisés (mais également des ``favicon`` ou des ``humans.txt``)
* | **Behaviour**: Tous les alias des options ``where`` et ``order_by`` de la méthode ``find()`` fonctionne quelques soit le niveau où l'alias est utilisé et même dans les méthodes de chainage.
  | Concerne : ``context`` dans ``Contextable``, ``published`` dans ``Publishable``, ``default_sort`` dans ``Sortable``, ``parent`` dans ``Tree`` et ``context_main`` dans ``Twinnable``.
* **Migration**: Ajout d'un ID incrémental et d'une date d'éxécution dans la table des migrations
* **App manager**: Les boutons sont désactivés après le clic pour éviter qu'il soit recliqué et que la même action s'exécute deux fois
* **Blog/News**: Ajout d'un titre spécifique pour la liste des billets d'un auteur
* **Blog/News**: Le ``page_title`` et le ``title`` des ``meta`` sont modifiés pour les listes de billets de catégorie, tag et auteur
* **Comments**: Le contexte du commentaire peut être passé par les paramètres dans l'API

Dépréciés
---------

* :ref:`release/migrate_from_chiba.2_to_d/i18n_crud_config`
* :ref:`release/migrate_from_chiba.2_to_d/hmvc`
* :ref:`release/migrate_from_chiba.2_to_d/loadConfiguration`
* :ref:`release/migrate_from_chiba.2_to_d/applicationRequiredFromMetadata`
* :ref:`release/migrate_from_chiba.2_to_d/extends.application`
* :ref:`release/migrate_from_chiba.2_to_d/extends.apps`
