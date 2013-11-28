Notes de la version Chiba 2
###########################

Nouveautés
==========

* Support de Windows à partir de Windows Vista
* Amélioration du wizard d'installation (interface, plus de tests, choix des langues)
* Permissions avancées dans les applications natives
* Application commentaires :

    * Interface d'administration
    * Quand un nouveau commentaire est posté, envoi d'un email à l'auteur du billet et aux autres commentateurs.

.. versionadded:: Chiba2.1

* L'ajout de media en masse.

Développeur
===========

Ruptures de compatibilité
-------------------------

* :ref:`release/migrate_from_chiba.1_to_chiba.2/model_dataset`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/crud_success`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/attachment`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/comments`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/blognews`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/getUrlEnhanced`

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

.. versionadded:: Chiba 2.1

* **Media**: Bugfix, les images transformées ne s'affichaient en front-office que pour les utilisateurs connectés au back-office. Les autres obtenaient un ``403``.
* **Media**: Bugfix dans les permissions des medias; quand un utilisateur était mis à jour, ces droits en écriture sur les médias étaient désactivés.
* **CRUD**: La configuration du boutton ``save`` n'est plus obligatoire dans la définition des champs d'un CRUD.
* **ORM**: Dans les modèles, si vous utilisez ``cache_model_properties``, nouvelle possibilité de définir une fonction de callback (``check_property_callback``, voir :file:`local/config/config.php.sample`) pour vérifier si une propriété est un potentiel nouveau champ, et ainsi éviter une requête SQL ``show field``.
* **Renderer**: Nouvelle classe ``Nos\Renderer`` pour factoriser du code entre tous les renderers.
* **Templates basic**: Réorganisation pour une meilleur factorisation de code entre les templates avec menu en haut et à gauche.
* **Slideshow**: Réorganisation de la configuration et des fichiers. Les widgets d'affichage en front-office sont gérés avec une configuration par formats pour être plus facilement étendables.
* **Blog/News and Comments**: Meilleur nettoyage du cache front-office quand un post ou un commentaire sont insérés, mis à jour ou supprimés.

.. versionadded:: Chiba 2.2

* **Renderer**: La classe Nos\Renderer_Date_Picker a été factorisée avec Nos\Renderer_Datetime_Picker
* **Media**: La suppression des media et des répertoires est géree par les modèles, et non plus par le controller CRUD
* **i18n**: Dans la classe i18n, ajout des méthodes addPriorityDictionary et addPriorityMessages
* **Tasks**: Les ``Tasks`` FuelPHP ont été adaptées à Novius OS. Le namespace des ``Tasks`` dépend maintenant de l'application ce qui permet de nommer de la même façon 2 ``Tasks`` dans des applications différentes.
             Un application, `novius_taskmanager <https://github.com/novius/novius_taskmanager>`__, a été réalisée permettant la gestion et l'exécution des ``Tasks`` via le navigateur.
* **Form**: Amélioration de la mise en page des emails de réponse à un formulaire.

.. versionadded:: Chiba 2.3

* **PHP**: La version 5.5 est officiellement supportée
* **Renderer**: Nouvelle option ``null_allowed`` (à ``false`` par défaut) pour ``Nos\Renderer_Datetime_Picker``
* **Misc**: Optimisation de ``Toolkit_Image->sizes()``, Les images des ``Media`` ne sont plus chargées en mémoire
* **WYSIWYG**: Dans la popup image, nouveaux champs border, align, vspace et hspace pour faciliter l'édition du style
* **CRUD**: Le javascript pour les ``context common fields`` est amélioré. Maintenant, les champs non supportés peuvent implémenter leur propre système de verrouillage
* **CRUD**: Le système de verrouillage des ``context common fields`` est amélioré. Maintenant il fonctionne aussi pour les champs non basés sur un input (ie: comme pour les renderers basés sur un ``<div>``)
* **CRUD**: Le système de verrouillage des ``context common fields`` supporte les champs basé sur le renderer virtual name
* **Profiler**: Certains items de la config ne sont plus affichés pour des raisons de sécurités
* **Profiler**: Nouvelles méthodes ``markDeltaStart()`` et ``markDeltaStop()`` pour l'étude des durées d'exécution
* **ORM**: Nouveau paramètre ``through_where`` dans la configuration des relations ``many_many``
* **Form**: Ajout d'un ``replyto`` aux emails envoyés si un champ email est présent dans la réponse. Dépend de la clé de configuration ``add_replyto_to_first_email`` du fichier ``noviusos_form.config.php`` (par défault à ``true``)
* **Form**: Déplacement du champ de l'émail destinataire en haut du formulaire d'administration
* **AppWizard**: Ajout d'une vérification préalable sur les droits d'écriture dans le dossier ``local/applications``

.. _release/chiba.2/deprecated:

Dépréciés
---------

* :ref:`release/migrate_from_chiba.1_to_chiba.2/enhancer`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/media`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/media_folder`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/page_link`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/user_login`

.. versionadded:: Chiba 2.1

* :ref:`release/migrate_from_chiba.1_to_chiba.2/renderer_selector`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/renderer_media`
* :ref:`release/migrate_from_chiba.1_to_chiba.2/slideshow`
