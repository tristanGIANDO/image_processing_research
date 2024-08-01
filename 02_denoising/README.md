# Reflexions sur le débruitage

## SOMMAIRE

#### I. Types de bruit

* Bruit Gaussien
* Bruit de Poisson
* Bruit impulsionnel
* Bruit uniforme

#### II. Techniques de débruitage

* **A. Filtres**
  * Filtre moyen
  * Filtre médian
  * Filtre gaussien

* **B. Statistiques**
  * PCA
    * Version de `sklearn`
    * _Ma version_
  * Non Local Means
    * Version de `opencv`
    * _Ma version_

* **C. Réseaux de neurones**
  * Auto encodeurs
  * CNNs

* **D. Débruiter des images plus complexes (EXR, 32 Bits Float...)**

___

### Introduction

Le débruitage d'images est une technique utilisée en traitement d'images pour réduire ou éliminer le bruit présent dans une image. Le bruit est une perturbation indésirable généralement introduite lors de l'acquisition de l'image par des capteurs électroniques.

Le débruitage d'images est crucial dans de nombreux domaines tels que :

* **Imagerie médicale** : Pour améliorer la clarté des images obtenues par radiographie, IRM, etc.
* **Photographie numérique** : Pour améliorer la qualité des photos prises dans des conditions de faible luminosité.
* **Surveillance et sécurité** : Pour améliorer les images des caméras de surveillance.
* **Astronomie** : Pour éliminer le bruit des images capturées par des télescopes.

### I. Types de Bruit

#### Bruit Gaussien

Bruit aléatoire suivant une distribution normale, souvent dû à des perturbations thermiques dans les capteurs.

#### Bruit de Poisson

Bruit dépendant de l'intensité du signal, typique dans les images acquises avec peu de lumière.

#### Bruit Impulsionnel (Sel et Poivre)

Apparition de pixels noirs et blancs aléatoirement répartis, souvent causé par des erreurs de transmission.

#### Bruit Uniforme

Bruit avec une distribution de probabilité uniforme sur une plage spécifique.

### II. Techniques de Débruitage

Les méthodes de débruitage peuvent être classées en plusieurs catégories principales :

#### A. Filtres (scipy)

##### Filtre Moyen

Chaque pixel est remplacé par la moyenne des pixels de son voisinage.

##### Filtre Median

Chaque pixel est remplacé par la médiane des pixels de son voisinage, efficace contre le bruit impulsionnel.

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/median_low.png)
!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/median_high.png)

##### Filtre Gaussien

Utilise une convolution avec une fonction gaussienne, réduisant le bruit gaussien de manière plus lisse.

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/gaussian_low.png)
!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/gaussian_high.png)

#### B. Statistiques

##### PCA

SKLearn PCA :
!["skpca"](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/PCA_sklearn.png)

Manual PCA
!["mypca"](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/PCA_custom.png)

* **SKLearn PCA :** 84.999 % in 0.119 seconds
* **My version of PCA :** -> 84.0344 % in 0.839 seconds

###### Testing on "lena_bruit.png" (RGB, 512*512px)

From this :

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/src/base_lena_bruit.png)

To this (my favourites are the green ones):
!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/patch_denoise_pca_median_gauss.jpg)

##### Non Local Means

Moyennage des pixels ayant des patchs similaires dans l'image, prenant en compte des pixels éloignés pour un meilleur lissage.
I was a little frustrated.
Despite the rather promising results, the quality of RGB denoising isn't really up to scratch with what we tested.

So I went looking for the best known software methods and discovered the **non-local means** method.

1. For each pixel, the NLM compares it with other pixels in the image, more or less distant.
2. A weight is then calculated based on the similarity between the patches centered around the target pixel and the comparison pixel. The more similar the patches, the higher the weight.
3. The target pixel is then replaced by a weighted average of all comparison pixels, using the calculated weights. This means that similar pixels have more influence on the final pixel value.

**Result : Detail is preserved!**

`open-cv` does this in one line and very quickly, but the aim of this project is to understand how it works. So I've redone my own version (which works even though it's _40 times_ slower!).

###### NLM openCV

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/NLM_opencv.png)

###### NLM custom

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/NLM_custom.png)

#### C. Réseaux de neurones

##### Autoencodeurs

Réseaux de neurones entraînés pour encoder puis décoder une image, apprenant à éliminer le bruit lors de la reconstruction.

##### CNNs (Convolutional Neural Networks)

Réseaux convolutifs spécialement conçus pour le débruitage d'images, exploitant des architectures profondes pour améliorer la qualité de l'image débruitée.

#### D. Débruiter des images plus complexes (EXR, 32 bits Float...)

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/src/base_rafale.jpg)

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/images/rafale.jpg)
