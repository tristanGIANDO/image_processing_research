# gt_denoiser

*A denoiser using gaussian, median filters and PCA*

## Goal

We go from this :
!["base"](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/base.png)
To this :
!["result](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/result.png)

___

## I. Making our own PCA

SKLearn PCA :
!["skpca"](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/skpca_pca.png)

Manual PCA
!["mypca"](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/mypca_pca.png)

### Performances :

**SKLearn PCA :** 84.999 % in 0.119 seconds

**My version of PCA :** -> 84.0344 % in 0.839 seconds
___

## II. Filters (scipy)

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

___
___

## III. Let's explore Non Local Means!

I was a little frustrated.
Despite the rather promising results, the quality of RGB denoising isn't really up to scratch with what we tested.

So I went looking for the best known software methods and discovered the **non-local means** method.

1. For each pixel, the NLM compares it with other pixels in the image, more or less distant.
2. A weight is then calculated based on the similarity between the patches centered around the target pixel and the comparison pixel. The more similar the patches, the higher the weight.
3. The target pixel is then replaced by a weighted average of all comparison pixels, using the calculated weights. This means that similar pixels have more influence on the final pixel value.

**Result : Detail is preserved!**

`open-cv` does this in one line and very quickly, but the aim of this project is to understand how it works. So I've redone my own version (which works even though it's *40 times* slower!).

!["."](https://raw.githubusercontent.com/tristanGIANDO/gt_denoiser/main/output/my_nlm.png)