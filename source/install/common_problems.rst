Problèmes courant d'installation
################################

.. sidebar:: Table of contents

    .. contents::
        :backlinks: top
        :depth: 2
        :local:

Htaccess non autorisé avec Apache
*********************************

Symptômes
---------

* Vous avez le message ``Your server does not allow .htaccess file``
* Vous utilisez Novius Os sur une serveur Apache
* Vous avez installé Novius OS dans un sous-répertoire d'un ``host``, généralement le ``host`` par défaut

Solution
--------

* Trouvez le fichier de configuration du ``virtualhost``, généralement dans :file:`/etc/apache2/site-enabled/`.
* Éditez le fichier de configuration du ``virtualhost`` avec les droits en écriture.

Dans cette exemple, nous utilisons l'éditeur :program:`nano` et le nom du fichier de configuration du ``virtualhost`` est :file:`000-default` :

.. code-block:: bash

    sudo nano /etc/apache2/site-enabled/000-default

Dans le fichier, trouvez la ligne ressemblant à (si Novius OS est installé dans le répertoire :file:`/var/www/` subdirectory)  :

.. code-block:: apache

    <Directory /var/www>
        AllowOverride None
        Options FollowSymLinks
    </Directory>

Changez ``AllowOverride None`` par ``AllowOverride All``. Sauvegardez vos changement et redémarrez Apache :

.. code-block:: bash

    sudo service apache2 restart

Droits d'écriture sur Windows
*****************************

Symptômes
---------

* Vous avez installé Novius OS sur Windows
* Vous avez des messages commençant par ``Give write permission to all users``

Solution
--------

Vous pouvez essayer de démarrer votre serveur :program:`WAMP` avec les privilèges administrateur.

Ou vous pouvez essayez de changer les droits d'accès sur le répertoire de Novius OS, et récursivement sur ces sous-répertoires.
Donner les droits d'écritures pour tout le monde (`Exemple pour windows 7 <http://www.wikihow.com/Change-File-Permissions-on-Windows-7>`__).
Essayez en redémarrant le serveur après.

Droits d'écriture en FTP
************************

Symptômes
---------

* Vous avez installé Novius Os en le transférant par FTP
* Vous avez des messages disant que les répertoires ``must be writeable``
* Vous ne pouvez pas exécuter les commandes données, vous n'avez pas accès au serveur via :program:`ssh`

Solution
--------

Vous pouvez donner les droits d'écriture avec votre logiciel FTP. Par exemple, ce `tutoriel pour Filezilla <http://www.dummies.com/how-to/content/how-to-change-file-permissions-using-filezilla-on-.html>`__

``chmod a+w`` veut dire donner les droits d'écriture à tous les utilisateurs.

Installation de GD sur Ubuntu
******************************

Symptômes
---------

* Vous avez le message ``GD is required``
* Vous utilisez Novius OS sur Ubuntu

Solution
--------

.. code-block:: bash

    sudo apt-get install php5-gd
    sudo apt-get install libgd2-xpm-dev*

Forbidden quand vous accédez au back-office
*******************************************

Symptômes
---------

* Après l'installation, quand vous essayez d'accéder au back-office, votre navigateur retourne une page disant ``Forbidden``

Ce problème existe notamment pour l'hébergeur ``Infomaniak.ch``

Solution
--------

Éditez le fichier :file:`.htaccess`. Changez la ligne :


.. code-block:: apache

    Options +FollowSymLinks -Indexes

Par :

.. code-block:: apache

    Options +FollowSymlinks -SymlinksIfOwnerMatch -Indexes


magic_quotes_gpc mus be off
****************************

Symptômes
---------

* Vous avec le message ``PHP configuration directive ‘magic_quotes_gpc’ must be off``
* Vous êtes sur un hébergement mutualisé ``OVH``

Solution
--------

Ajoutez cette ligne au fichier :file:`.htaccess` :

.. code-block:: apache

    SetEnv MAGIC_QUOTES 0

