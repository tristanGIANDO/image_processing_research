Une image numérique est une représentation visuelle d'informations sous forme électronique, que l'on peut afficher sur des écrans ou imprimer. Contrairement aux images traditionnelles qui sont physiques, comme les photographies argentiques ou les peintures, les images numériques sont constituées de données numériques. Voici quelques éléments clés qui définissent une image numérique :


### 1. **Pixels et Matrices**

Une image numérique est composée de petits éléments appelés pixels (de l'anglais "picture elements"). Chaque pixel représente une petite partie de l'image et possède une couleur et une luminosité spécifique. La résolution d'une image, c'est-à-dire sa clarté et son détail, est souvent mesurée en nombre de pixels horizontaux et verticaux (par exemple, 1920x1080 pixels).

Une image numérique peut être vue comme une matrice \( M \) de dimensions \( m \times n \), où \( m \) est le nombre de lignes (hauteur de l'image) et \( n \) est le nombre de colonnes (largeur de l'image). Chaque élément \( M_{i,j} \) de la matrice représente un pixel à la position \( (i, j) \) dans l'image.

Par exemple, pour une petite image en noir et blanc de 3x3 pixels, la matrice \( M \) pourrait être :

\[ M = \begin{bmatrix}
0 & 255 & 0 \\
255 & 0 & 255 \\
0 & 255 & 0
\end{bmatrix} \]

Dans cet exemple, les valeurs 0 et 255 représentent les niveaux de gris (0 étant le noir, 255 le blanc), ce qui est typique pour une image en échelle de gris avec une profondeur de couleur de 8 bits (256 niveaux possibles de gris).

### 2. **Couleurs et Modèle RVB (RGB)**

Pour une image en couleur, chaque pixel est représenté par trois valeurs correspondant aux canaux Rouge (R), Vert (G), et Bleu (B). Ces trois valeurs sont souvent stockées sous forme de triplets \( (R, G, B) \) et peuvent être combinées pour représenter une large gamme de couleurs.

Par exemple, pour une image couleur 2x2, la matrice pourrait être :

\[
M = \begin{bmatrix}
(255, 0, 0) & (0, 255, 0) \\
(0, 0, 255) & (255, 255, 0)
\end{bmatrix}
\]

Ici, \( (255, 0, 0) \) représente le rouge pur, \( (0, 255, 0) \) le vert pur, \( (0, 0, 255) \) le bleu pur, et \( (255, 255, 0) \) le jaune (combinaison de rouge et vert).

### 3. **Profondeur de Couleur**

La profondeur de couleur est le nombre de bits utilisés pour représenter la couleur d'un seul pixel. Par exemple, une image en couleur 24 bits (8 bits par canal) peut représenter \( 2^{24} \) (environ 16,7 millions) de couleurs différentes. Cela signifie que chaque composant de couleur (R, G, B) peut prendre une valeur de 0 à 255.

### 4. **Codage de l'image et Formats de Fichiers**

Les images numériques sont souvent compressées et enregistrées dans divers formats pour économiser de l'espace de stockage. Par exemple, le format JPEG utilise une compression avec perte, ce qui signifie que certaines informations de couleur sont perdues pour réduire la taille du fichier. Le format PNG utilise une compression sans perte, conservant toute l'information originale.

### **Exemple de Codage d'une Image**

Considérons une simple image en noir et blanc de 2x2 pixels avec les valeurs suivantes:

\[
M = \begin{bmatrix}
0 & 255 \\
255 & 0
\end{bmatrix}
\]

Pour coder cette image en un fichier binaire, chaque pixel peut être converti en une valeur binaire de 8 bits :

- \( 0 \) devient \( 00000000 \)
- \( 255 \) devient \( 11111111 \)

L'image complète peut être stockée sous forme d'une séquence binaire :

\[
00000000 \, 11111111 \, 11111111 \, 00000000
\]

Cela donne une représentation numérique compressée de l'image.
Les images numériques peuvent également inclure des métadonnées, qui sont des informations supplémentaires sur l'image, comme la date de création, l'appareil photo utilisé, les paramètres de prise de vue, et parfois des informations sur les droits d'auteur.

En résumé, une image numérique est une matrice de pixels, chaque pixel ayant des valeurs numériques spécifiques pour représenter des couleurs ou des niveaux de gris. Ces valeurs sont stockées dans des fichiers numériques et peuvent être manipulées mathématiquement pour modifier l'image.
