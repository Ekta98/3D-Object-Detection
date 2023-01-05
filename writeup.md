# Self-Driving Car Beta Testing Nanodegree 

This is a template submission for the midterm second course in the Udacity Self-Driving Car Engineer Nanodegree Program : 3D Object Detection (Midterm). 


## 3D Object detection

We have used the [Waymo Open Dataset's](https://console.cloud.google.com/storage/browser/waymo_open_dataset_v_1_2_0_individual_files) real-world data and used 3d point cloud for lidar based object detection. 

- Configuring the ranges channel to 8 bit and view the range /intensity image (ID_S1_EX1)
- Use the Open3D library to display the lidar point cloud on a 3d viewer and identifying 10 images from point cloud.(ID_S1_EX2)
- Create Birds Eye View perspective (BEV) of the point cloud,assign lidar intensity values to BEV,normalize the heightmap of each BEV (ID_S2_EX1,ID_S2_EX2,ID_S2_EX3)
- In addition to YOLO, use the [repository](https://review.udacity.com/github.com/maudzung/SFA3D) and add parameters ,instantiate fpn resnet model(ID_S3_EX1)
- Convert BEV coordinates into pixel coordinates and convert model output to bounding box format  (ID_S3_EX2)
- Compute intersection over union, assign detected objects to label if IOU exceeds threshold (ID_S4_EX1)
- Compute false positives and false negatives, precision and recall(ID_S4_EX2,ID_S4_EX3)


The project can be run by running the command

```
python loop_over_dataset.py
```

The code implementation is done in:
loop_over_dataset.py
student/objdet_pcl.py
student/objdet_detect.py
student/objdet_eval.py


## Step-1: Compute Lidar point cloud from Range Image

#Visualize range image channels (ID_S1_EX1)

![image](https://user-images.githubusercontent.com/28135189/210700033-cebc01a0-9d02-4333-b477-ed603ca6ae86.png)

The result will look like:
![image](https://user-images.githubusercontent.com/28135189/210700257-81b2cbc8-d428-42c6-8919-06172136f6e1.png)

#Visualize lidar point-cloud (ID_S1_EX2)

![image](https://user-images.githubusercontent.com/28135189/210700395-12170e06-8691-4fd3-9692-44b560dce89e.png)

The result will look like:

![image](https://user-images.githubusercontent.com/28135189/210700514-31bfa5b7-31b6-46e3-80f1-df7d4152dc92.png)

![image](https://user-images.githubusercontent.com/28135189/210700543-fbad925f-d692-4b54-86b7-483ca8fcd640.png)

![image](https://user-images.githubusercontent.com/28135189/210700576-bb5c8215-5a9e-47af-b536-d7c7d548a92b.png)

![image](https://user-images.githubusercontent.com/28135189/210700610-5a3449a6-8626-4e49-af20-fe12461ba8bd.png)

![image](https://user-images.githubusercontent.com/28135189/210700657-dfcfaa41-f529-44af-ae93-64a1c9eeaf70.png)

![image](https://user-images.githubusercontent.com/28135189/210700687-407f044d-485a-42f8-b514-8f0df5e78bd8.png)

![image](https://user-images.githubusercontent.com/28135189/210700723-988b42da-4a2d-4869-b08b-8d9560db6e47.png)

Above we can see few images with examples of vehicles with varying degrees of visibility in the point-cloud.

We can see that stable features include the tail lights and the rear bumper. In some cases the additional features include the headover lights, car front lights, rear window shields vehicle tyres etc are also seen. These are identified through the intensity channels.

## Step-2: Creaate BEV from Lidar PCL

Convert sensor coordinates to BEV-map coordinates (ID_S2_EX1)

![image](https://user-images.githubusercontent.com/28135189/210701382-731a9c46-ce2a-4dae-8d67-062ae4318449.png)

The result will look like:

![image](https://user-images.githubusercontent.com/28135189/210701449-35895a05-64f3-4604-bb96-582b7bd2715f.png)

Compute intensity layer of the BEV map (ID_S2_EX2)

![image](https://user-images.githubusercontent.com/28135189/210701521-b72607a2-b045-453c-b126-36f020fbbda4.png)

The result will look like:

![image](https://user-images.githubusercontent.com/28135189/210702307-c1f5ca8b-ef5d-4bbf-a6d4-f0052d4b7d8b.png)

Compute height layer of the BEV map (ID_S2_EX3)

![image](https://user-images.githubusercontent.com/28135189/210702369-8fe44478-90cd-443f-9a43-5a3ee3437596.png)

The result will look like:

![image](https://user-images.githubusercontent.com/28135189/210702440-584894e5-46e6-489a-95ce-4f871edf00ee.png)

##Section 3 : Model-based Object Detection in BEV Image

Here we are using the cloned [repo](https://github.com/maudzung/SFA3D) ,particularly the test.py file  and extracting the relevant configurations from 'parse_test_configs()'  and added them in the 'load_configs_model' config structure.

- Instantiating the fpn resnet model from the cloned repository configs
- Extracting 3d bounding boxes from the responses
- Transforming the pixel to vehicle coordinates
- Model output tuned to the bounding box format [class-id, x, y, z, h, w, l, yaw]

![image](https://user-images.githubusercontent.com/28135189/210702547-cd09a648-11d6-41e8-a722-0908528daa6b.png)

#Extract 3D bounding boxes from model response (ID_S3_EX2)

![image](https://user-images.githubusercontent.com/28135189/210702612-ab44f297-3823-4c97-ab28-30ddd03fa691.png)

The result lokks like:

![image](https://user-images.githubusercontent.com/28135189/210702724-eda4eed2-dbd2-42a4-87b7-2ad93b83efe0.png)

##Section 4 : Performance Evaluation for Object Detection

#Compute intersection-over-union between labels and detections (ID_S4_EX1)

![image](https://user-images.githubusercontent.com/28135189/210702860-cc3564b3-ec8f-4e2b-8290-9c2eb375e221.png)

#Compute false-negatives and false-positives (ID_S4_EX2)

#Compute precision and recall (ID_S4_EX3)

![image](https://user-images.githubusercontent.com/28135189/210703011-9bb452fa-9710-49a7-94df-59d99e47cc22.png)

Results:
![image](https://user-images.githubusercontent.com/28135189/210703086-0126cd44-04f2-4aa3-abb2-3e69d2a1d170.png)

![image](https://user-images.githubusercontent.com/28135189/210703125-67aa7436-95b0-41f9-8f29-cf257631f90f.png)

Set the flag configs_det.use_labels_as_objects to True

![image](https://user-images.githubusercontent.com/28135189/210703324-c2f2ba19-bf6d-4686-8e51-8705539bad64.png)


![image](https://user-images.githubusercontent.com/28135189/210703276-b8deecb6-a15a-4ee0-a32c-44896d2aa1c8.png)







