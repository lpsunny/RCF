## [Richer Convolutional Features for Edge Detection](http://mmcheng.net/rcfedge/)

### Introduction

In this paper, we propose an accurate edge detector using richer convolutional features (RCF). Since objects in natural images possess various scales and aspect ratios, learning the rich hierarchical representations is very critical for edge detection. CNNs have been proved to be effective for this task. In addition, the convolutional features in CNNs gradually become coarser with the increase of the receptive fields. According to these observations, we attempt to adopt richer convolutional features in such a challenging vision task. The proposed network fully exploits multiscale and multilevel information of objects to perform the image-to-image prediction by combining all the meaningful convolutional features in a holistic manner. Using VGG16 network, we achieve state-of-the-art performance on several available datasets. When evaluating on the well-known BSDS500 benchmark, we achieve ODS F-measure of 0.811 while retaining a fast speed (8 FPS). Besides, our fast version of RCF achieves ODS F-measure of 0.806 with 30 FPS.

### Citations

If you are using the code/model/data provided here in a publication, please consider citing our paper:

    @article{liu2019richer,
      title={Richer Convolutional Features for Edge Detection},
      author={Liu, Yun and Cheng, Ming-Ming and Hu, Xiaowei and Bian, Jia-Wang and Zhang, Le and Bai, Xiang and Tang, Jinhui},
      journal={IEEE Transactions on Pattern Analysis and Machine Intelligence (TPAMI)},
      volume={41},
      number={8},
      pages={1939--1946},
      year={2019},
      publisher={IEEE}
    }

    @inproceedings{liu2017richer,
      title={Richer Convolutional Features for Edge Detection},
      author={Liu, Yun and Cheng, Ming-Ming and Hu, Xiaowei and Wang, Kai and Bai, Xiang},
      booktitle={IEEE conference on computer vision and pattern recognition (CVPR)},
      pages={3000--3009},
      year={2017}
    }

### PyTorch version of RCF
For the pytorch implementation of RCF, please refer to this [github repository](https://github.com/meteorshowers/RCF-pytorch). Thanks for Yuanyi's contribution!

### Evaluation results

Evaluation results for BSDS500 and NYUD datasets are available [here](http://mftp.mmcheng.net/liuyun/rcf/eval.tar).

**We have released the code and data for plotting the edge PR curves of many existing edge detectors [here](https://github.com/yun-liu/plot-edge-pr-curves).**

The precomputed edge maps for BSDS500 dataset is available [here](https://drive.google.com/drive/folders/1jFRGTY9QtSYcM3fC6U86KWO1OmeSZCgZ?usp=sharing).

### Pretrained models

RCF model for BSDS500 dataset is available [here](http://mftp.mmcheng.net/liuyun/rcf/model/rcf_pretrained_bsds.caffemodel).

RCF model for NYUD dataset is available here ([Depth](http://mftp.mmcheng.net/liuyun/rcf/model/rcf_pretrained_nyud_depth.caffemodel) and [Image](http://mftp.mmcheng.net/liuyun/rcf/model/rcf_pretrained_nyud_image.caffemodel)).

### Testing RCF

1. Clone the RCF repository
    ```Shell
    git clone https://github.com/yun-liu/rcf.git
    ```

2. Download pretrained models, and put them into `$ROOT_DIR/examples/rcf/` folder.

3. Download the datasets you need as below, and extract these datasets to `$ROOT_DIR/data/` folder.

    ```bash
    wget http://mftp.mmcheng.net/liuyun/rcf/data/bsds_pascal_train_pair.lst
    wget http://mftp.mmcheng.net/liuyun/rcf/data/HED-BSDS.tar.gz
    wget http://mftp.mmcheng.net/liuyun/rcf/data/PASCAL.tar.gz
    wget http://mftp.mmcheng.net/liuyun/rcf/data/NYUD.tar.gz
    ```

4. Build Caffe.

5. Go into the folder `$ROOT_DIR/examples/rcf/`. Then, you can run RCF-singlescale.ipynb to test single-scale RCF on BSDS500 dataset, or run RCF-multiscale.ipynb to test multiscale RCF on BSDS500 dataset, or run RCF-singlescale-NYUD.ipynb to test single-scale RCF on NYUD dataset.

Note: Before evaluating the predicted edges, you should do the standard non-maximum suppression (NMS) and edge thinning. We used Piotr's Structured Forest matlab toolbox available [here](https://github.com/pdollar/edges).

### Training RCF

1. Download the datasets you need.

2. Download the pretrained vgg16 model [here](http://mftp.mmcheng.net/liuyun/rcf/model/5stage-vgg.caffemodel).

3. Start training process by running following commands:

    ```Shell
    cd $ROOT_DIR/examples/rcf/
    ./train.sh
    ```

### ResNet version of RCF

The code for the ResNet version of RCF has been released. The pretrained ImageNet and BSDS500 models are available [here](https://drive.google.com/drive/folders/18X4vDHUTRjmyfDIC0Bbr2gDsQR2KEi7d). Some discussion can be found under the [issue #89](https://github.com/yun-liu/rcf/issues/89).

### What is the "AutoCrop" layer?

The "AutoCrop" layer in RCF can caculate the crop offset automatically, and the recent version of Caffe doesn't support this. In fact, we can calculate the crop offset by ourselves, so we can replace the "AutoCrop" layer with the standard Crop layer in Caffe by setting the offsets to 1, 2, 4, and 0 for conv2, conv3, conv4, and conv5, respectively. More details can be found under the [issue #24](https://github.com/yun-liu/rcf/issues/24).

### Acknowledgment

This code is based on HED. Thanks to the contributors of HED.

    @inproceedings{xie2015holistically,
      title={Holistically-nested edge detection},
      author={Xie, Saining and Tu, Zhuowen},
      booktitle={Proceedings of the IEEE International Conference on Computer Vision},
      pages={1395--1403},
      year={2015}
    }
