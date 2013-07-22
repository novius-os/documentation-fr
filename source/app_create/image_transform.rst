Afficher mes vignettes dans différents formats
##############################################

Vous avez ajouté des vignettes à votre mode modèle. Maintenant vous voulez les afficher en front-office.

En mode liste, vous voulez les afficher couper avec une taille fixe de 150x150 pixels et en noir et blanc.


Dans votre vue de liste :

.. code-block:: php
   :emphasize-lines: 4-6

    <?php

    foreach ($items as $item) {
        echo $item->thumbnail->getToolkitImage()->crop_resize(150, 150)->grayscale()->html(array(
            'style' => 'float:right;'
        ));
        echo '<h2><a href="', $item->url(), '">', e($item->title), '</a></h2>';
    }

En mode fiche, vous voulez affiche la vignette de l'item avec un largeur maximale de 300 pixels et
une hauteur maximale de 200 pixels, et une légère rotation de 15 degrés.

Dans votre vue de liste :

.. code-block:: php
   :emphasize-lines: 3

    <?php

    echo $item->thumbnail->getToolkitImage()->shrink(300, 200)->rotate(15)->html();
    echo '<h1>', e($item->title), '</h1>';
    echo '<p>', e($item->description), '</p>';

.. seealso::    :ref:`La classe Toolkit_Image pour plus de possibilités <api:php/classes/toolkit_image>`.
