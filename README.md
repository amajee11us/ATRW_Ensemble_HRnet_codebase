# Tiger Pose Estimation - Ensemble learning on HRNet
An ensemble technique applied on High Resolution net to improve accuracy on pose detection task.
This project was carried out as a part of CVWC-2019 for ICCV 2019 - Amur Tiger re-Identification challenge.

#### Challenge overview - https://cvwc2019.github.io/challenge.html

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
### Folder structure for dataset
```diff
HEAD
|__data
   |__tiger
      |__images
      |  |__train
      |  |__test
      |  |__val
      |__annotations
         |__<train_annotations>
         |__<test_annotations>
         |__bb_predictions_pose_test.json <GT bboxes for test dataset>
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
## Running the Experiments
The experiment requires you to create 5 directories named output1, output2.... These will store the trained output models.
The trained models are fed to a predictor which runs evaluation on the val/test dataset to obtain the final outputs.
The outputs and the GTs are passed to the evaluator script which scores and returns the performance metrics to us.
To run the above mentioned scenario do the following:
1. Create your conda environment from the '.yaml' file provided in the root directory.
```diff
conda env create -f pose-env.yaml
```
2. Go to the ```lib ``` directory and run ``` make ```. This builds the nms library
3. Also install pycocotools 
4. Your basic setup is ready.

### Training the 5-Fold training model
Run the following command:
```diff
python tools/train.py \
    --cfg experiments/coco/hrnet/w32_256x192_adam_lr1e-3.yaml
 ```
 Remember to change the config file path to suite your requirements.
 
 ### Test a sample
 ```diff
 python tools/test.py \
    --cfg experiments/coco/hrnet/w32_256x192_adam_lr1e-3.yaml
  ```
## References
```diff
@inproceedings{sun2019deep,
  title={Deep High-Resolution Representation Learning for Human Pose Estimation},
  author={Sun, Ke and Xiao, Bin and Liu, Dong and Wang, Jingdong},
  booktitle={CVPR},
  year={2019}
}

@inproceedings{xiao2018simple,
    author={Xiao, Bin and Wu, Haiping and Wei, Yichen},
    title={Simple Baselines for Human Pose Estimation and Tracking},
    booktitle = {European Conference on Computer Vision (ECCV)},
    year = {2018}
}
```
