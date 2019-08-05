# Tiger Pose Estimation - Ensemble learning on HRNet
An ensemble technique applied on High Resolution net to improve accuracy on pose detection task.

## Method Description
The key aspect of our approach was to improve on the corner cases on already effective HRNet network. For this reason, the following methodology was adopted:
1. We conducted experiments with multi resolution images to test the effect of resolution on      the model. We finally settled on 640x480 input size. 
2. During training we adopted a 5 fold split on the entire train+validation dataset. 
3. For improving the accuracy during inference, the 5 fold split was ensembled using multiple      approaches - average ensemble, bagging  ensemble and random forest ensemble for obtaining      the best results from the solution. For the submission we have selected average ensemble as    it performed the best in our experiments.
4. All the models used we trained on HRNet-W32 network which were pre-trained on ImageNet          dataset.

### Folder structure for pretrained model
```diff
HEAD
|__models
   |__pytorch
      |__imagenet
         |__hrnet_w32-36af842e.pth
```
### Folder structure for output directory (Taken care by the code)
```diff
HEAD
|__output (or whatever name was specified in the config or Notebook)
   |__<dataset>
       |__pose_hrnet
          |__<config>
             |__contains results and intermediate training results
```
