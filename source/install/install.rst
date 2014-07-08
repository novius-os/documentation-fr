Installation
############

.. sidebar:: Sommaire

	.. contents::
		:backlinks: top
		:depth: 2
		:local:

Prérequis généraux
******************

Disposer d'un serveur avec MySQL et PHP 5.3+

Novius OS tourne aussi bien sur :

* :program:`Linux`, :program:`Mac OS` que :program:`Windows` (à partir de Vista)
* :program:`Apache` avec le **mod_rewrite** activé ou :program:`Nginx`

LAMP
====

Nous décrivons ci-après la procédure d'installation sur un serveur :program:`LAMP` (Linux/Apache/MySQL/PHP), de type :program:`Debian`,
sur lequel vous avez les droits d'administration. À adapter à votre configuration.

* Installation de :program:`AMP`

	.. code-block:: bash

			sudo apt-get install apache2 php5 mysql-server libapache2-mod-php5 php5-mysql

* Activer le **mod_rewrite** d’:program:`Apache`.

	.. code-block:: bash

			sudo a2enmod rewrite

Installation rapide
*******************

Pré-requis
==========

* Avoir un accès ligne de commande sur le serveur et disposer des droits d'administration :command:`sudo`.
* Avoir :program:`Git` installé.

Installation
============

Ouvrez un terminal et saisissez :

.. code-block:: bash

    cd /var/www
    sudo wget http://raw.github.com/novius-os/ci/master/dubrovka/tools/install.sh && sh install.sh

À la question :guilabel:`« Enter the directory name where you want to install Novius OS (default novius-os) »`,
indiquez le nom du répertoire dans lequel vous voulez installer votre instance de Novius OS.
Laissez vide pour l'installer dans un répertoire :file:`novius-os`.

Une fois l'installation terminée :

* Ouvrez votre navigateur à l'URL :file:`http://votredomaine/novius-os/` (remplacez :file:`novius-os` par le nom du répertoire que vous avez saisi).
* Poursuivez l'installation avec :doc:`l'assistant de paramétrage <setup_wizard>`.

.. note::

	* Pour une installation en local, l'URL sera probablement :file:`http://localhost/novius-os/`.
	* Si le ``DOCUMENT_ROOT`` de votre serveur n'est pas :file:`/var/www/`, modifiez la première ligne en conséquence.

Installation via Zip
********************

Cette procédure est à privilégier si vous souhaitez installer Novius OS sur un hébergement mutualisé :

* Téléchargez  `novius-os.4.3-dubrovka.zip <http://nova.li/nov4-3>`__.
* Dézippez le fichier.
* Uploadez (ou déplacer) le répertoire :file:`novius-os` dans le ``DOCUMENT_ROOT`` de votre serveur (par exemple via FTP).
* Ouvrez votre navigateur à l'URL :file:`http://votredomaine/novius-os/` (remplacez :file:`novius-os` par le nom du répertoire où vous avez dézippé Novius OS).
* Poursuivez l'installation avec :doc:`l'assistant de paramétrage <setup_wizard>`.


Installation avancée
********************

Configuration d'un Virtual Host
===============================

Les commandes suivantes sont données à titre d'exemple si vous voulez installer Novius OS sur Ubuntu, adaptez les en fonction de votre distribution.

.. code-block:: bash

	sudo nano /etc/apache2/sites-available/novius-os.conf

| Remplacez :command:`nano` par n'importe quel autre éditeur de texte.
| Remplacez :file:`novius-os.conf` par le nom que vous voulez donner à votre ``Virtual Host``.

| Copiez la configuration suivante dans le fichier que vous venez d'ouvrir et sauvegardez.
| Adaptez la ligne ``ServerName`` avec votre nom de domaine dans le cas d'une installation en production.
| De même, remplacez :file:`/var/www/novius-os` par le répertoire dans lequel vous avez installé Novius OS.

.. code-block:: apache

	<VirtualHost *:80>
		DocumentRoot /var/www/novius-os/public
		ServerName   novius-os
		<Directory /var/www/novius-os/public>
			AllowOverride All
			Options FollowSymLinks
		</Directory>
	</VirtualHost>

La configuration par défaut contient un répertoire :file:`public`. C'est vers ce lui que doit pointer ``DocumentRoot``.

Activez votre nouveau ``VirtualHost`` :

.. code-block:: bash

	sudo a2ensite novius-os.conf

Relancez ensuite :program:`Apache` pour appliquer la nouvelle configuration.

.. code-block:: bash

	sudo service apache2 reload

Configurer le fichier hosts, dans le cas d'installation sur votre machine
-------------------------------------------------------------------------

Si vous installez Novius OS sur votre machine locale, vous devez ajouter une ligne au fichier :file:`/etc/hosts`, avec la valeur du ``ServerName`` (``novius-os`` dans l'exemple ci-desssus) .

.. code-block:: bash

	sudo nano /etc/hosts

Ajouter la ligne suivante :

.. code-block:: bash

	127.0.0.1   novius-os

Installation avancée avec Git
=============================

Il faut cloner le dépôt disponible sur GitHub :

.. code-block:: bash

	git clone --recursive git://github.com/novius-os/novius-os.git

Cette commande télécharge le dépôt principal, avec plusieurs submodules :

* novius-os : le cœur de Novius OS, qui contient lui-même des submodules, comme fuel-core ou fuel-orm.
* Différents submodules dans :file:`local/applications` : les applications blog, actualités, commentaires, formulaires, diaporamas...

| La branche par défaut du dépôt pointe vers la dernière version stable.
| Les nouvelles versions seront disponibles dans des nouvelles branches.

| Pour le moment, tous les dépôts dépendants de novius-os/novius-os partagent le même numéro de version.
  C'est-à-dire qu'une application disponible sur notre compte Github existe dans les mêmes versions que le cœur de Novius OS.
  Donc si vous utilisez ``novius-os/core`` en version |version|, alors vous devriez aussi utiliser ``novius-os/app`` dans le même numéro de version |version|.

| Pour changer la version que vous voulez utiliser après un clone, n'oubliez pas de mettre à jour les submodules !
| Exemple qui utilise la dernière nightly de la branche ``dev`` :

.. code-block:: bash

	cd /var/www/novius-os/
	git checkout dev
	git submodule update --recursive

Installation sur serveur Nginx
==============================

Exemple de configuration :program:`Nginx` :

.. literalinclude:: nginx.txt
