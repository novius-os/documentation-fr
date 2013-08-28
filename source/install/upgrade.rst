Mise à jour
###########

Mise à jour des fichiers
************************

Git
====

Si vous avez installé Novius OS avec :program:`Git`, placez-vous dans le répertoire de votre Novius OS :

.. code-block:: bash

	git fetch origin
	git checkout master/chiba2
	git submodule update --recursive --init

.. note::

    La mise à jour des ``submodules`` peut afficher une ligne

    .. code-block:: bash

        warning: unable to rmdir packages/log: Le dossier n'est pas vide

    si c'est le cas, exécutez la commande suivante :

    .. code-block:: bash

        rm -rf novius-os/packages/log/

Zip
====

Si vous avez téléchargé Zip, la procédure est plus complexe.

* Mettons que votre Novius OS est installé dans :file:`monsite/`.
* Faites une sauvegarde de votre répertoire (copiez le répertoire ou zippez le).
* Téléchargez le `nouveau zip de Novius OS <http://www.novius-os.org/download-novius-os-zip.html>`__ et dézippez-le.
  Vous avez un répertoire :file:`novius-os/`.
* Dans :file:`monsite/`, détruisez les répertoires suivant :
	* :file:`monsite/novius-os/`
	* Tous les répertoires :file:`monsite/local/applications/noviusos_*`

* Copiez les répertoires et fichiers suivant de :file:`novius-os/` vers :file:`monsite/` :
	* :file:`novius-os/`
	* Tous les répertoires :file:`local/applications/noviusos_*`
	* Tous les fichiers :file:`local/config/*.sample`
	* :file:`public/htdocs/install/`, :file:`public/htdocs/install.php` et :file:`public/htdocs/migrate.php.sample`
	* Tous les fichiers à la racine du répertoire

Vous pouvez alors continuer votre mise à jour.

Lancer la migration
*******************

Avant de lancer la procédure de migration automatique, sauvegarder votre base de données.

Via SSH
=======

Si vous avez accès à :program:`SSH` sur le serveur, placez-vous dans le répertoire de votre Novius OS :

.. code-block:: bash

	sudo php oil refine migrate
	sudo php oil refine migrate -m

Via Navigateur
==============

Si vous n'avez pas accès à :program:`SSH`, vous pouvez faire la migration via votre navigateur :

* Au préalable vous devez renommer le fichier :file:`public/migrate.php.sample` en :file:`public/migrate.php`.
* Appelez ensuite ce fichier via son URL, par exemple :file:`http://www.monsite.com/migrate.php`.

Via l'interface back-office
===========================

Si vous n'avez pas accès à :program:`SSH`, vous pouvez faire la migration via l'interface d'administration de votre Novius OS :

* Connectez-vous à votre back-office
* Ouvrez l'application "Gestion des applications"
* Cliquer sur "Prendre en compte les changements" pour toutes les applications, ou sur "Actualiser toutes les metadata" dans la barre d'outils si vous êtes en mode expert.

.. warning::

    Quand vous allez accéder à votre back-office sans avoir lancé les migrations, votre logiciel sera dans un état instable.
    Les sources ne correspondront pas avec l'état de la base de données. Vous aurez sans doute des messages d'erreur.
    Vous pouvez les ignorer.

Mettre à jour vos développement
*******************************

Si vous avez des développements personnels, suivez la procédure le :doc:`/release/migrate_from_chiba.1_to_chiba.2`.
