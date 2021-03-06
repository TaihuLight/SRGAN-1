# SRGAN
A PyTorch implementation of SRGAN based on the paper 
[Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network](https://arxiv.org/pdf/1609.04802.pdf)

## Requirements
- [Anaconda](https://www.anaconda.com/download/)
- PyTorch
```
conda install pytorch torchvision -c pytorch
```
- tqdm
```
pip install tqdm
```
- opencv
```
conda install -c anaconda opencv
```

## Datasets

### Train、Val Dataset
The train and val datasets are sampled from [VOC2012](http://cvlab.postech.ac.kr/~mooyeol/pascal_voc_2012/).
Train dataset has 16700 images and Val dataset has 425 images.
Download the datasets from [here](https://pan.baidu.com/s/1c17nfeo), and then extract it into `data` directory.

### Test Dataset
The test dataset are sampled from 
| **Set 5** |  [Bevilacqua et al. BMVC 2012](http://people.rennes.inria.fr/Aline.Roumy/results/SR_BMVC12.html)
| **Set 14** |  [Zeyde et al. LNCS 2010](https://sites.google.com/site/romanzeyde/research-interests)
| **BSD 100** | [Martin et al. ICCV 2001](https://www.eecs.berkeley.edu/Research/Projects/CS/vision/bsds/)
| **Sun-Hays 80** | [Sun and Hays ICCP 2012](http://cs.brown.edu/~lbsun/SRproj2012/SR_iccp2012.html)
| **Urban 100** | [Huang et al. CVPR 2015](https://sites.google.com/site/jbhuang0604/publications/struct_sr).
Download the dataset from [here](https://pan.baidu.com/s/1nuGyn8l), and then extract it into `data` directory.

## Usage

### Train
```
python train.py

optional arguments:
--crop_size           super resolution crop size [default value is 88]
--upscale_factor      super resolution upscale factor [default value is 4](choices:[2, 4, 8])
--g_threshold         super resolution generator update threshold [default value is 0.3](choices:[0.2, 0.3, 0.4, 0.5, 0.6, 0.7])
--g_stop_threshold    super resolution generator update stop threshold [default value is 2](choices:[1, 2, 3])
--num_epochs          super resolution epochs number [default value is 100]
```
The output val super resolution images are on `images` directory.

### Test Benchmark Images
```
python test_benchmark.py

optional arguments:
--upscale_factor      super resolution upscale factor [default value is 4]
--model_name          super resolution model name [default value is netG_epoch_4_100.pth]
```
The output super resolution images are on `results` directory.

### Test Single Image
```
python test_image.py

optional arguments:
--upscale_factor      super resolution upscale factor [default value is 4]
--image_name          low resolution image name
--model_name          super resolution model name [default value is netG_epoch_4_100.pth]
```
The output super resolution images are on the same directory.

### Test Video
```
python test_video.py

optional arguments:
--upscale_factor      super resolution upscale factor [default value is 4]
--is_real_time        super resolution real time to show [default value is False]
--delay_time          super resolution delay time to show [default value is 1]
--model_name          super resolution model name [default value is netG_epoch_4_100.pth]
```
The output high resolution videos are on `results` directory.

## Benchmarks
The reconstructions of the digit numbers are showed at right and the ground truth at left.
<table>
  <tr>
    <td>
     <img src="results/ground_truth.jpg"/>
    </td>
    <td>
     <img src="results/reconstruction.jpg"/>
    </td>
  </tr>
</table>

Default PyTorch Adam optimizer hyperparameters were used with no learning rate scheduling. 
Epochs with batch size of 100 takes ~2 minutes on a NVIDIA GTX 1070 GPU. 

