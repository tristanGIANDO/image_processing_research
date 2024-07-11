# gt_denoiser

*A denoiser using gaussian, median filters and PCA*

## Results

We go from this :
!["base"](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/base.png)
To this :
!["result](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/result.png)

___

## Making our own PCA

SKLearn PCA :
!["skpca"](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/skpca_pca.png)

Manual PCA
!["mypca"](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/mypca_pca.png)

### Performances :

**SKLearn PCA :** 84.999 % in 0.119 seconds

**My version of PCA :** -> 84.0344 % in 0.839 seconds
___

## Filters (scipy)

#### Gaussian filter :

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/gaussian_low.png)
!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/gaussian_high.png)

#### Median filter :
!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/median_low.png)
!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/median_high.png)

___

## Testing on "lena_bruit.png" (RGB, 512*512px)

From this :
!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/src/lena_bruit.png)

To this (my favourites are the green ones):
!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/lena_bruit_denoise_tests_01.jpg)