# Face Recognition

Melissa Sh. Cotrina
https://github.com/Sheedy21/casa0018.git

## Introduction

Face recognition is a system that has gained more attention in recent years due to the capacity that this technology has to identify the human face. To achieve this, it is necessary to have a set of images to train the object detector considering the different factors like the model, data size, image size, etc. These features can help us get a more accurate object detector. However, what if we have an image or video frame that no contains the whole face. Will it be possible to recognize that as a face?.
For this reason, I used the Object Detection API to identify some parts of the face as a first step to detect a human face in an image. A model which can recognize people who are using masks or glasses. With these results, we won't need to train the model with other images, and we will be able to get the exact number of people in a specific space. And then, it can be extended to consider the same method to identify other objects. To give a simple example that can reflect the importance of this work is the use of our smartphones that are not able to recognize a face if it is showed partially. In the picture below, we can observe that eight of the nine people are recognized.

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/people1.jpg)


## Research Question

The research question of this work is how to identify a human face from an image or video frame more accurately.

## Application Overview

This project was built considering three fundamental building blocks. Moreover, it was included some suggestions received from the presentation. 

- Input: To train this model was necessary a set of images with different sizes to run the different experiments.

- Processing and storing: In this step was consider different environments to process the data and train the model. With all the images downloaded, it was used Jupyter notebook to get some descriptive statistics of the data. Then, all the images were standardized using a script in Anaconda prompt and labeled using LabelImg. Once all the information was labeled, it was split into two folders (train and test), and then, they were exported in two csv files to generate the TFRecords. Another file created to train the model was the label map that contains all the label information. And the last and most important file that contains all the information and parameters used to train the model is the config file which was modified considering my information. For the next step, the data and all the input files were stored in a Github repository. Finally, the training of the model was performed in Google Colab. 

- Output: Once the data was processed, the model was evaluated considering short videos based on the probability of recognition for each object detected. 

The diagram below summarizes all the procedures that have been done in this work.

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/diagram1.jpg)


## Data

The data used on this project was downloaded from Google images to have a variety of images for the first two experiments and extracted a sample from Kaggle's CelebFaces Attributes Dataset to perform the third experiment. To download the photos from Google images was used the Image Downloader extension. To analyze the information of the three datasets, I created the script "resize_image.py" to get some statistics of the data and standardize all the images. The tables below show the descriptive statistics of the data utilized in the three experiments. For the first one was used 55 images with a high variation between the image sizes. The average size was 193x144 pixels before the standardization; after that, the images were resized, getting a size of 193x161 on average. For the second experiment was included larger images with a mean size of 509x429 pixels. After resizing them, there was not a significant difference in the mean size (509x513 pixels). In the case of the third experiment, it was not necessary to resize the images because all the data was already clean, showing an average size of 178x218 pixels. Once all the images were standardized, they were split for the training (90%) and testing data (10%).

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/statistics1.jpg)

## Model

The model used in the three experiments was SSD MobileNet V2, the single-stage detection model, which is part of the Tensorflow object detection API. According to the description of this model, the architecture is characterized by the thin bottleneck layers of the input and output of the residual block (Francis). Furthermore, the SSD network is followed by several convolution layers. I consider this model because it just needs one shot to detect various objects (Liu, Wei, et al., 2016). In the case of the first two experiments, it was considered the three parts of the face (eye, nose, and mouth), while in the third, it was just considered the whole face.

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/model.jpg)


## Experiments

In this work was considered three experiments and to perform them was necessary to generate the input files to train the models. As it was mentioned in the application overview, there were several scripts that were used and some files that were modified.

The models created in this project were built following the steps performed by Gilbert Tanner. 

Once we got all the information, it was necessary to label each image using LabelImg. For the first two experiments, it was essential to specify each part of the face that was analyzed, while for the third experiment was considered the whole face. It is important to mention that this procedure took a lot of time to label all the images because it has to be done manually. For this reason, at the beginning was considered small datasets to train the models. The images below show these steps.

Experiment 1 and 2:

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/label22.jpg)

Experiment 3:

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/label11.jpg)


With all the images labeled, they were divided for the train and test data. For this step was used two scripts from Dat Tran’s raccoon detector. The first file is "xml_to_csv.py" which exports two csv files, one for the train data and the other for the test data. The other script used was "generate_tfrecord.py" which generates the TFRecords files.

The next file that we need to create is the "label_map.pbtxt", this file contains all the labels with their respective id and description. Finally, the last file that we need to consider is the "pipeline_fname.config". This file is found in the sample folder of the Tensorflow repository; in this folder, we have to select the config file of the model that we want to use to train the object detector. In this file, we have to change the number of classes or objects that we want to recognize, three for the two first experiments and one class for the last experiment. We also have to change the path of the label_map and TFRecords files.

For the next step, it was used the script "tensorflow_custom_object_detection_vf.ipynb" created by Chengwei which was developed to run in Google Colab. This code was adapted to run the three experiments iteratively in this cloud service because of the different configurations and the type of processor that this environment supports. Once the code was executed, we need to export the models for future evaluations.

The following parameters were considered for the three experiments:

- Number of training steps: 1000
- Number of evaluation steps: 50
- Number of layers: 6
- Number of classes: 3 (Experiment 1 and 2) and 1 (Experiment 3)
- Batch size: 24
- Sample size: 55 (Experiment 1 and 2) and 500 (Experiment 3)

To evaluate the performance of the models, we have to run the "%tensorboard --logdir=training" function. In this case, it was considered the "loss" to evaluate the models.

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/tensorboard1.jpg)

As we know, the first two models contemplate the three parts of the face (eye, nose, and mouth) with the difference in the average size of the images. Comparing both models, we can observe that the first model shows a lower loss of 3.90. However, if we compare this model with the third one, we can see that this last model enhances presenting a loss of 2.65. This improvement can be caused for the larger data size considered in the third experiment. 

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/loss1.jpg)

To test the models, it was used the code from Zszazi's Object detection to evaluate considering a short videos. In the first one, we can see that the model isn't able to identify the parts of the face accurately. It can have happened because the data which was used to train the model contained smaller images compared with the other two.

[![Watch the video](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/exp_11.jpg)](https://www.youtube.com/watch?v=qmy4xwmZLA4)

In the second experiment, the model improved because it was able to detect the parts of the face but no the three at the same time.

[![Watch the video](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/exp_22.jpg)](https://www.youtube.com/watch?v=ck8igFbP0yk)

In the last experiment, the model was evaluated in a group of people walking on the street. In this case, the images considered to train this model were faces taken from different angles; that's why the model was able to recognize more faces.

[![Watch the video](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/exp_33.jpg)](https://www.youtube.com/watch?v=qLuPpmfNz08)

## Model deployment

For the deployment of the models as Edge AI, the Tensorflow Lite app lets use the custom object detector in Android and iOS considering an input image size of (300x300x3). We don't need to change the initial model that was used to train the object detectors because the architecture was designed for mobile devices. I couldn't replicate it on my smartphone because it didn't meet the requirements. 

## Results and Observations

According to the results of the three experiments, we can see that the size of the images considered to train the model can impact the process of face recognition. Another factor that could affect the performance of the first two models is the number of images considered to train the object detector. In these experiments, it was just considered 55 images per each one because this process was done manually, and I had to select two eyes, one nose, and one mouth per image in most cases. Even though the first model had a lower final loss compared with the second one, this late one was able to recognize the parts of a face more precisely. However, one problem with this model would be that this can't distinguish between the eyes of a person and an animal. 

Concerning the last experiment, the model was able to recognize various faces with different probabilities of response. Combining the last two models, we can conclude that to get a more accurate model is necessary to train the object detector with partial faces, not with too small parts like the eye, nose, or mouth but with larger parts of the face like in the graphs below.

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/face_div1.jpg)

As it was said before, the models were trained in Google Colab, taking some time to adapted the code and run the three models in this environment. Even though this cloud service has a good processor, it has limited usage, which didn't let me work fast.

## Bibliography


1. Chengwei, 2021. Blog | DLology. [online] Dlology.com. Available at: <https://www.dlology.com/blog/author/Chengwei/> [Accessed 30 March 2021].

2. GitHub. 2021. datitran/raccoon_dataset. [online] Available at: <https://github.com/datitran/raccoon_dataset> [Accessed 30 March 2021].

3. GitHub. 2021. tensorflow/models. [online] Available at: <https://github.com/tensorflow/models> [Accessed 30 March 2021].

4. GitHub. 2021. zszazi/Object-detection-in-video. [online] Available at: <https://github.com/zszazi/Object-detection-in-video/blob/master/ObjectDectection_in_Video.ipynb> [Accessed 30 March 2021].

5. Kaggle.com. 2021. CelebFaces Attributes (CelebA) Dataset. [online] Available at: <https://www.kaggle.com/jessicali9530/celeba-dataset> [Accessed 30 March 2021].

6. Liu, Wei et al., 2016. SSD: Single Shot MultiBox Detector. Computer Vision – ECCV 2016, 9905, pp.21–37.

7. Resources.wolframcloud.com. 2021. SSD-MobileNet V2 - Wolfram Neural Net Repository. [online] Available at: <https://resources.wolframcloud.com/NeuralNetRepository/resources/SSD-MobileNet-V2-Trained-on-MS-COCO-Data#:~:text=SSD%2DMobileNet%20V2%20Trained%20on%20MS%2DCOCO%20Data&text=Released%20in%202019%2C%20this%20model,box%20coordinates%20and%20class%20probabilities.&text=This%20model%20is%20part%20of%20the%20Tensorflow%20object%20detection%20API.> [Accessed 30 March 2021].

8. Tanner, G., 2021. Creating your own object detector with the Tensorflow Object Detection API. [online] Gilberttanner.com. Available at: <https://gilberttanner.com/blog/creating-your-own-objectdetector> [Accessed 30 March 2021].


## Declaration of Authorship

I, MELISSA COTRINA SALAS, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.


Melissa Sh. Cotrina
01/04/2021