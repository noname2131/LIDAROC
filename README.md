# News
Realistic LiDAR Cover Contamination Dataset for Enhancing Autonomous Vehicle Perception Reliability

# Download
The dataset will be available upon acceptance to IEEE Sensor Letter Journal. 
The dataset is provided on-demand, by sending a request. 

# LIDAROC
Realistic LiDAR Cover Contamination Dataset for Enhancing Autonomous Vehicle Perception Reliability


# Sensor and Ego-Vehicle
Data collection is carried out using a real testbed car equipped with the Robosense reference system. We use RS-Ruby as our LiDAR
sensor with specification 128 beam, minimum 0.1 degrees Vertical Angular Resolution, Horizontal resolution 0.2 degrees, 250 meters range, Horizontal FoV 360 degrees, Vertical FoV 40 degrees, frame rate 10 Hz. This LiDAR generates at least 2.3 million point/second and support for L4+ autonomous driving.  

# Target Object
<img src="https://github.com/noname2131/LIDAROC/blob/main/images/5m-environment.jpeg" width="300" height="200">


# LiDAR Cover Contamination
<img src="https://youtu.be/kBRiJ5zdWXkg" width="300" height="200">


# Object Detection Benchmark
We tested this data using five state-of-the-art object detection method taken from model zoo https://github.com/thu-ml/3D_Corruptions_AD/tree/main/OpenPCDet/OpenPCDet#model-zoo
, listed below:
1. PointRCNN
2. SECOND
3. PointPillar
4. PartA2
5. PV_RCNN
6. 3DSSD

All of the model trained using KITTI dataset, then we use default parameters from [Dong, Yinpeng, et al. "Benchmarking Robustness of 3D Object Detection to Common Corruptions." Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition. 2023.]  

For the benchmarking results, PointRCNN, SECOND, and PointPillar were successful in detecting objects using our data, and we have included these results in this repository for an analysis of the effects of contamination. However, both PartA2 and PV_RCNN failed to detect any targets in this dataset, so we have marked them as failures and have not included them in the table.  

PV_RCNN was unable to detect objects because it depends on specific parameters, such as Keypoints, which need to be finely tuned beforehand. In the case of PartA2, each object class should be tuned for its own predefined anchors, given the significant variation in object sizes across different classes. We avoided tuning these hyperparameters because our objective for this benchmarking work was not to re-train the models. Instead, we aimed to test models trained on clean LiDAR data and then assess their performance on contaminated LiDAR data to understand the impact of contaminants on object detection. 
 
Additionally, since the 3DSSD model was not provided, we were unable to test it on our dataset.

Our focus is on evaluating state-of-the-art (SOTA) methods for LiDAR data corruption due to cover contamination. We introduce two new evaluation parameters: 'Corner Case' and 'Instability', the latter also referred to as 'Undetected Frames'. Based on the table provided in this repository, we conclude that PointRCNN demonstrates the best performance, showing the smallest performance penalty in both the 10-meter and 20-meter datasets for detecting Car and Pedestrian. For a detailed explanation, please refer to our paper titled 'CleanScan: Real-Time Contaminant Detection in LiDAR Systems for Reliable Autonomous Vehicle Perception'.

Example of Detection Result using PointRCNN. We chose PointRCNN \cite{Shi_2019_CVPR} as our benchmarking object detection since PointRCNN showed the best performance in terms of the lowest RCE (relative corruption error) by measuring the performance drop over synthetic corruption \cite{dong2023benchmarking}.
