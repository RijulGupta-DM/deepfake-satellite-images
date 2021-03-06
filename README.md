# deepfake-satellite-images
## _By DeepMedia_


[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/Naereen/StrapDown.js/graphs/commit-activity) [![Linux](https://svgshare.com/i/Zhy.svg)](https://svgshare.com/i/Zhy.svg)

[![forthebadge cc-nc-sa](http://ForTheBadge.com/images/badges/cc-nc-sa.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0) 

[DeepMedia][dm] is setting the standard for responsible use of synthetic media technology. Here, we present the DM-AER-DeepFake-V1 dataset that includes over 1M images of synthetic aerial images. Details about the dataset, creation methods, and initial detection results are presented below.

## DM-AER-DeepFake-V1 Dataset
- Contains 1M DeepFake Aerial Images
- Contains 120K Real Aerial Images

The DM-AER-DeepFake-V1 dataset is split into sample, validation, and training folders. The real images are a part of the [Million-AID][million-aid] dataset. These images were not present during the creation of the synthetic images. The synthetic images are generated by DeepMedia. The sample folder contains images from the validation set, but there is no overlap in images between the validation and training sets. The data can be downloaded at this google drive location.

https://drive.google.com/drive/folders/1h65vVQvfYzMsmofxTTEIOVSIWdi7zjTo?usp=sharing

## Dataset Creation
The DM-AER-DeepFake-V1 dataset was created by training the [rosinality StyleGAN2][ros] repo on the [AID dataset][aid] of aerial images. The software was trained an NVIDIA V100 GPU for 14 days until 800K steps. The following parameters were adjusted from their default values:

- architecture: swagan
- d_reg_every: 4
- added learning rate scheduler
- augmentation

<p float="left">
  <img src="https://user-images.githubusercontent.com/104281028/164993812-c6b3512a-919d-44b2-9b83-6e6069691af1.png" width="256" />
  <img src="https://user-images.githubusercontent.com/104281028/164993815-bca1c534-b674-44f3-b68f-64e0b8e1cf0c.png" width="256" /> 
  <img src="https://user-images.githubusercontent.com/104281028/164993823-742292ef-1bc9-4208-af77-af4eb5e3c981.png" width="256" />
</p>

## Detection
Initial detection experiments were run on the initial 1M fake images generated. The [ViT-pytorch][vit] repo was chosen as a state-of-the-art detection method. The real AID dataset was used as the "authentic" image source. The repo's dataloader module was modified to ensure upsampling of the authentic images so that the model would see equal number of authentic and fake images during training. The network converged after 2 days of training on an NVIDIA V100 GPU. High-level results are presented below:
- accuracy: 97%
- Type 1 error: 04%
- Type 2 error: 02%


<img width="540" alt="Screen Shot 2022-04-24 at 12 54 09 PM" src="https://user-images.githubusercontent.com/104281028/164994148-6614d336-9c5c-4be8-a3b9-2159161fca11.png">
<img width="443" alt="Screen Shot 2022-04-24 at 12 44 08 PM" src="https://user-images.githubusercontent.com/104281028/164994108-528166f1-392e-4669-8e44-86125858e60e.png">
<img width="419" alt="Screen Shot 2022-04-24 at 12 44 19 PM" src="https://user-images.githubusercontent.com/104281028/164994067-e8326074-885f-4b8e-8209-59a1bf2fa8ab.png">




Additionally, class activation maps were implemented in the ViT network and ran on both authentic and fake aerial images in order to better understand what image features provided the most contextual information in order to lead to ViT convergence.

<img width="627" alt="Screen Shot 2022-04-24 at 12 44 44 PM" src="https://user-images.githubusercontent.com/104281028/164994005-c6a3afca-34ce-4772-9bbb-5e98a928b897.png">


## Future Research
These results depict an early exploration into the creation and detection of synthetic aerial images. Below, we attempt to provide a non-exhaustive list of areas for potential improvement in creation methods, as well as techniques for detection.
- Integrate the Million-AID into synthetic aerial image creation 
- Integrate higher resolution input images
- Integrate a more diverse set of input images
- Retrain StyleGAN2 with hyper-parmater grid search to achieve higher quality results
- Transition from StyleGAN2 to StyleGAN3 to achieve higher quality results
- Retrain at 1024x1024 resolution, or higher
- Integrate projection-based networks to enable targeted manipulation of aerial imagery
- Integrate higher-information images, just as 12bit/16bit/etc
- Investigate and reproduce initial ViT results
- Investigate more advanced detection methods

## Acknowledgements
DeepMedia hopes to set the standard for ethical and responsible use of synthetic media technology, but we can't do this alone. We would like to thank the investors, government organizations, and academic instutions that are helping make this possible. 

For more information, please send a message to contact@deepmedia.ai


[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dm]: <https://www.deepmedia.ai/>
   [million-aid]: <https://arxiv.org/pdf/2006.12485v2.pdf>
   [ros]: <https://github.com/rosinality/stylegan2-pytorch>
   [aid]: <https://captain-whu.github.io/AID/>
   [vit]: <https://github.com/jeonsworld/ViT-pytorch>

