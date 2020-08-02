# multisensorOpticalCDUsingCycleGAN
Change detection in VHR multisensor optical images via CycleGAN based adaptation

For the main change detection code, please refer to DCVA (https://github.com/sudipansaha/dcvaVHROptical) <br/>
Let us assume, images X_A and X_B are acquired over the same place at two different time by two different VHR optical sensors A and B. Our final goal is to detect change between X_A and X_B.
The steps to run the multi-sensor CD are: <br/>
**Create dataset for CycleGAN training**: Extract patches that are acquired by sensors A and B and are collected from the same area (or areas with similar characteristics). These patches are not same as X_A and X_B and not to be confused. Please refer to the paper for more details. <br/>  Number of patches should be atleast few hundred for effective CycleGAN training <br/>
**CycleGAN training**: Use the above patches to train cycleGAN (details in: https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix) <br/>
**The two generators**: After cycleGAN training, the two generators G_AB and G_BA will be reused for change detection <br/>
**Projecting X_A to the domain of sensor B**: In the code of deep change vector analysis (https://github.com/sudipansaha/dcvaVHROptical), use G_AB to project X_A to the domain of sensor B. This can be achieved by: <br/>
inputToNetDate1Transcoded=G_AB(inputToNetDate1)
<br/>
In the code of DCVA, this is to be done before the following line
obtainedFeatureVals1=layerWiseFeatureExtractorFunction[outputLayerNumber](inputToNetDate1)
**Using G_BA as deep feature extractor**: In the code of DCVA (https://github.com/sudipansaha/dcvaVHROptical), simply use G_BA as deep feature extractor instead of the pre-trained network.




### Citation
If you find this code useful, please consider citing:
```[bibtex]
@inproceedings{saha2019unsupervisedMultisensor,
  title={Unsupervised Multiple-Change Detection in VHR Multisensor Images Via Deep-Learning Based Adaptation},
  author={Saha, Sudipan and Bovolo, Francesca and Bruzzone, Lorenzo},
  booktitle={IGARSS 2019-2019 IEEE International Geoscience and Remote Sensing Symposium},
  pages={5033--5036},
  year={2019},
  organization={IEEE}
}
```
