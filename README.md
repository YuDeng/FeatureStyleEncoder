## A Style-Based GAN Encoder for High Fidelity Reconstruction of Images and Videos

Official implementation for paper: A Style-Based GAN Encoder for High Fidelity Reconstruction of Images and Videos. 

[[Video Editing Results]](https://drive.google.com/file/d/1ebih6TZxb2eLKxJdbO8GnsInDKSegfYL/view?usp=sharing)

![teaser](images/teaser.png)

> **Abstract** We propose a novel architecture for GAN inversion, which we call Feature-Style encoder. The style encoder is key for the manipulation of the obtained latent codes, while the feature encoder is crucial for optimal image reconstruction. Our model achieves accurate inversion of real images from the latent space of a pre-trained style-based GAN model, obtaining better perceptual quality and lower reconstruction error than existing methods. Thanks to its encoder structure, the model allows fast and accurate image editing. Additionally, we demonstrate that the proposed encoder is especially well-suited for inversion and editing on videos. We conduct extensive experiments for several style-based generators pre-trained on different data domains. Our proposed method yields state-of-the-art results for style-based GAN inversion, significantly outperforming competing approaches. 


## Requirements

### Dependencies

- Python 3.6
- PyTorch 1.8
- Opencv

You can install a new environment for this repo by running
```
conda env create -f environment.yml
conda activate feature_style
```

### Prepare StyleGAN2 model and other necessary models

* We adapt the StyleGAN2 model implemented by paper [Encoding in Style: a StyleGAN Encoder for Image-to-Image Translation](https://arxiv.org/pdf/2008.00951.pdf). Here is their [official implementation](https://github.com/eladrich/pixel2style2pixel.git). 

* Download and save the pretrained models running
    ```
    sh download_models.sh
    ```


## Training

* Prepare the training data

    To train the encoder for StyleGAN, we use the synthetic images generated by StyleGAN and also the real images [ffhq dataset](https://github.com/NVlabs/ffhq-dataset).
    You can generate the synthetic images by running
    ```
    python generate_imgs.py
    ```
    and download the ffhq dataset (aligned faces) to `data/ffhq-dataset/images/`.
    
* Training

    You can modify the training options of the config file in the directory `configs/`.
    ```
    python train.py --config 001 
    ```

## Testing 

* Inversion

    You can test the encoder on the images in `test/`. The output images are saved in `output/image/`.
    ```
    python test.py --pretrained_model_path './pretrained_models/143_enc.pth' --input_path './test/'
    ```
* Inversion and editing in notebook

    You can explore the encoder and the attribute editing code in notebook `inference.ipynb`. You can also open it in Google Colab [here](https://colab.research.google.com/github/InterDigitalInc/FeatureStyleEncoder/blob/master/inference.ipynb). 


## Video Manipulation

We provide a script to achieve inversion and attribute manipulation for the videos in the test directory `data/video/`. You can upload your own video and modify the options in `run_video_inversion_editing.sh`.

```
sh run_video_inversion_editing.sh
```

## Citation
```
@article{xuyao2022,
  title={A Style-Based GAN Encoder for High Fidelity Reconstruction of Images and Videos},
  author={Yao, Xu and Newson, Alasdair and Gousseau, Yann and Hellier, Pierre},
  journal={European conference on computer vision},
  year={2022}
}
```
## License

Copyright © 2022, InterDigital R&D France. All rights reserved.

This source code is made available under the license found in the LICENSE.txt in the root directory of this source tree.




