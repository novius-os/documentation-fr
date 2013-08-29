Notes de la version Chiba 2
###########################

Nouveautés
==========

* Support de Windows à partir de Windows Vista
* Amélioration du wizard d'installation (interface, plus de tests, choix des langues)
* Permissions avancées dans les applications natives
* Application commentaires :

    * Interface d'administration
    * Emails are sent when new comments are posted, to post author and others commenters.


Développeur
===========

Ruptures de compatibilité
-------------------------

* :ref:`release/migrate_from_chiba.1_to_chiba.2/model_dataset`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/crud_success`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/attachment`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/comments`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/blognews`

Mise à jour des librairies tierces
----------------------------------

* FuelPHP 1.6
* jQuery 1.9.1
* jQuery UI 1.10.3
* Wijmo 2013v1.4
* require.js 2.1.6


Améliorations
-------------
* **i18n**: :doc:`Le dictionaire par défaut </app_create/translate>` ``app::default`` est utilisé si aucun dictionaire n'a été configuré avec ``Nos\I18n::current_dictionary()``.
* **BD**: Changement de l'interclassement sur toutes les colonnes utilisées comme un identifiant d'URL.
* **ORM**: Amélioration du mécanisme de cache des ``properties`` de modèles, une seule récupération des colonnes via la BD par exécution.
* **ORM**: 4 nouveaux type de relation, :ref:`twinnable_belongs_to <api:php/relations/twinnable_belongs_to>`, :ref:`twinnable_has_one <api:php/relations/twinnable_has_one>`, :ref:`twinnable_has_many <api:php/relations/twinnable_has_many>`, :ref:`twinnable_many_many <api:php/relations/twinnable_many_many>`.
* **ORM**: Classe Model, nouvelles méthodes ``addRelation()``, ``configModel()`` et ``getApplication()``.
* **Behaviour**: Nouveau :ref:`behaviour author <api:php/behaviours/author>`, utilisé par Page, Media, Blog/News, Slideshow, Form.
* **Behaviour**: Refactoring de l'implémentation des ``behaviours`` (:ref:`Les behaviours peuvent intercepter des évènements de modèle <api:php/behaviours/behaviour_event>`).
* **Behaviour Twinnable**: Les modèles peuvent avoir des :ref:`champs <api:php/behaviours/twinnable/configuration>`, :ref:`medias et WYSIWYGs <api:php/models/model/configuration>` communs à tous les contextes.
* **Behaviour Twinnable**: new ``findMainOrContext()``, ``hasCommonFields()``, ``isCommonField()`` :ref:`methods <api:php/behaviours/twinnable/methods>`.
* **Behaviour URLEnhancer**: :ref:`Nouvelles méthodes <api:php/behaviours/urlenhancer/methods>` ``deleteCacheEnhancer()`` et ``deleteCacheItem()``.
* **Behaviour URLEnhancer**: Suppression du cache fron-office de l'item à la suppression et la mise à jour.
* **Enhancer**: Dans la configuration de la popup, nouvelle :doc:`possibilité de définir</app_create/enhancer>` ``layout`` et ``fields`` au lieu d'utiliser une ``view``, comme pour le CRUD.
* **Enhancer**: Dans la :ref:`configuration de l'enhancer <api:metadata/enhancers>`, nouvelle clé possible ``valid_container``, de type ``callable``. Permet de restreindre la disponibilité de l'enhancer en fonction du conteneur.
* **Enhancer**: Dans l'affichage front-office, la sortie de l'enhancer est enveloppée dans un ``div`` avec les classes CSS ``noviusos_enhancer`` et le nom de l'enhancer (``noviusos_blog``, ``noviusos_news``, ``noviusos_slideshow``, ``noviusos_form``)
* **Renderer**: Nouveau renderer :ref:`datetime picker <api:php/renderers/datetime>` pour gérer à la fois la date et l'heure dans le même ``input``.
* **WYSIWYG**: :ref:`Nouveau mécanisme de configuration des WYSIWYGs <api:php/configuration/wysiwyg>`, avec un événement ``wysiwygOptions`` interceptable par les behaviours (et utilisé par ``twinnable``), et un exemple de fichier ``wysiwyg`` de configuration.
* **WYSIWYG**: Dans ``Nos::parse_wysiwyg()``, le remplacement des ancres par ``URL#anchor`` se fait seulement en front-office.
* **SEO**: :ref:`Nouveau méchanisme de configuration des friendly slug <api:php/configuration/friendly_slug>`, avec un évenement ``friendlySlug`` interceptable par les behaviours (et utilisé par ``twinnable``), et un exemple de fichier ``friendly_slug`` de configuration.
* **OsTabs**: :ref:`Nouvelle méthode reload <api:javascript/$container/nosTabs>` dans l'API.
* **OsTabs**: Changement dans la position d'ouverture des onglets. Un onglet ouvert sans index s'ouvre maintenant ``onglet sélectionné + 1``, sauf si l'onglet sélectionné est le bureau, l'ouverture se fait à la dernière position.
* **Appdesk**: Deux nouvelles clés, ``css`` et :ref:`notify <api:php/configuration/application/appdesk/notify>` dans la :ref:`configuration des appdesk <api:php/configuration/application/appdesk>`.
* **Appdesk**: Possibilité d'ignorer un :ref:`cellFormatter <api:php/configuration/application/cellFormatters>` basé sur la valeur d'une colonne.
* **Appdesk**: Des :ref:`cellFormatters personnalisés <api:php/configuration/application/cellFormatters/custom>` sont autorisés dans les appdesks.
* **Grid**: Nouvelle clé ``align`` dans la :ref:`configuration des actions <api:php/configuration/application/common/actions>`.
* **Grid**: Nouvelle option pour définir la :ref:`profondeur d'ouverture initiale <api:php/configuration/application/appdesk/appdesk>` pour les ``treeGrid``.
* **UI**: Utilisation de ``.ui-priority-primary`` plutôt que ``.primary`` sur les ``button`` et de ``.title`` sur les ``textbox``.
* **UI**: Utilisation des select, checkbox et radio natifs du navigateur, plus aucune utilisation des widgets Wijmo pour ces ``inputs``.
* **Page**: L'assignation de la page d'accueil n'est plus permise en vue multi-contextes.
* **Page**: La suppression et la dépublication de la page d'accueil ne sont plus autorisés.
* **Page**: Augmentation du nombre de caractères autorisés dans les champs title et url.
* **Media**: Nouveau champ ``filesize``. Affichage du poids et des dimensions dans la prévisualisation de l'appdesk preview dans le formulaire de CRUD.
* **Media**: Refactoring des méthodes ``get_img_tag()`` et ``get_img_tag_resized()`` de :ref:`Model_Media <api:php/models/media/model_media/methods>`, utilisation de ``HTML::img()`` pour renvoyer un tag avec des attributs.
* **Media**: Vous pouvez maintenant transformer (crop, rotate, rounded, watermark, resize, shrink, grayscale, border) les images des Media et des Attachments avec le :ref:`Toolkit_Image API <api:php/classes/toolkit_image>`.
* **Media**: Nouvelle action "Régénérer le cache média" dans la barre d'outils de l'appdesk des Media, visible pour les utilisateurs en mode expert.
* **Media**: Augmentation du nombre de caractères autorisés dans les champs title et url.
* **Comments**: Nouvelle API pour l'utilisation de l'application ``noviusos_comments``.
* **Form**: Nouvelle ``view`` ``message`` pour la confirmation.
* **Blog/News**: :ref:`Les vignettes sont maintenant configurable (taille et lien) <api:applications/noviusos_blognews>`.
* **Misc**: Nouveaux événements :ref:`404.mediaFound <api:php/events/404.mediaFound>`, :ref:`404.attachmentFound <api:php/events/404.attachmentFound>`, :ref:`admin.loginFail <api:php/events/admin.loginFail>` et :ref:`nos.deprecated <api:php/events/nos.deprecated>`.
* **Misc**: Toutes les URL sont maintenant encodées quand utilisées dans un ``href`` ou une redirection.
* **Misc**: Nouveau répertoire ``temp`` dans :file:`local/data`, assigné à la clé de configuration :ref:`novius-os.temp_dir <api:php/configuration/software>` par défaut.
* **Front**: ``is_preview`` n'est vrai que si l'utilisateur est connecté.

.. _release/chiba.2/deprecated:

Dépréciés
---------

* :ref:`release/migrate_from_chiba.1_to_chiba.2/enhancer`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/media`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/media_folder`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/page_link`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/user_login`
