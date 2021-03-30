# Report title goes here

Melissa Sh. Cotrina

## Introduction

Face recognition is a system that has gained more attention in last years due to the capacity that this technology has to identify the human face. To achieve this, it is necessary to have a set of images to train the model considering the different factors like the model, data size, image size, etc. that can help us to get a more accurated object detector. However, what if we have an image or video frame that no contains the whole face, will it be possible to recognize that as a face. For this reason, I use the Object Detection API to recognize some parts of the face as a first step to detect a face in an image. This model can help us also to recognize people who are using masks or glasses. Whit these results, we can get the exact number of people that are in a specific space. And then, it can be extended to consider the same method to identify different objects. To give a simple example that can reflect the importance of this work is the use of our smartphones that are not able to recognize a face if it is showed parcially. In the picture below we can observe that eight of the nine people are recognized.

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/people.jpg)


## Research Question

The research question of this work is how to identify a human face from an image or video frame more accurately.

## Application Overview

This project was built considering three key building blocks and some suggestions received from the presentation. 

- Input: To train this model was necessary a set of images with different sizes which were downloaded from Google images instead of taking pictures to have a variety of images. To automathize this process was necessary to use the Image Downloader extension.

- Processing and storing: In this step was consider different enviroments to process the data and to train the model. With all the images downloaded, it was used jupyter notebook to get some descriptive statistics of the data; and then, all the images were standarized running a script in Anaconda prompt and labeled using LabelImg. In this procedure, it is important to mention that it took a lot of time to label all the images because we have to especify the object from the image. For this reason, at the beginning was considered a small dataset. Once, all the information was labeled, it is splitted in two folders (train and test) and then, they are exported in two csv files to generate the TFRecords. For this step was used two scripts from Dat Tran’s raccoon detector. Another important file that contains all the information required to train the model is the config file. This file was modified following the steps performed by Gilbert Tanner. For the next step, the clean data and all the input files were stored in a Github repository to train the model using a script created by Chengwei which was performed in Google Colab. This code was adapted to run the  experiments iteratively in this cloud service because of the different configurations and the type of processor that this environment supports.

- Output: Once the data was processed, the model was evaluated considering short videos based on the probability of recognition for each object detected. For this step was used the code from zszazi's Object detection to evualate video frames.

The diagram below summarizes all the procedures that have been done in this work.

![alt text](https://github.com/Sheedy21/casa0018/raw/main/Assessment/Reports/images/diagram.jpg)


## Data

Tha data use on this project was downloaded from Google images using the Image Downloader extension 
Describe what data sources you have used and any cleaning, wrangling or organising you have done. Including some examples of the data helps others understand what you have been working with.

*probably ~200 words and images of what the data 'looks like' are good!*

## Model
This is a Deep Learning project! What model architecture did you use? Did you try different ones? Why did you choose the ones you did?

*probably ~200 words and a diagram is usually good to describe your model!*

## Experiments
What experiments did you run to test your project? What parameters did you change? How did you measure performance? Did you write any scripts to evaluate performance? Did you use any tools to evaluate performance? Do you have graphs of results? 

*probably ~300 words and graphs and tables are usually good to convey your results!*

## Results and Observations
Synthesis the main results and observations you made from building the project. Did it work perfectly? Why not? What worked and what didn't? Why? What would you do next if you had more time?  

*probably ~300 words and remember images and diagrams bring results to life!*

## Bibliography
*If you added any references then add them in here using this format:*

1. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

2. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

----

## Declaration of Authorship

I, AUTHORS NAME HERE, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.


*Digitally Sign by typing your name here*

ASSESSMENT DATE
