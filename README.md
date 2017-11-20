#**Behavioral Cloning** 

##Writeup Template
---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

Architecture used in my pipeline: NAVIDA Architecture
 ![image](https://github.com/Genzaiwuxian/term1-p3/blob/master/cnn-architecture-624x890.png)

####1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* Term1-p3.ipynb containing the script to create and train the model, and generate 'model.h5' file used for AD in simulator
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* README.md: summarizing the results
* Video.mp4: the output video during the simulator runing under 'model.h5' file

####2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
by typing 'python driving.py model.h5'

####3. Submission code is usable and readable

The Term1-p3.ipynb file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

###Model Architecture and Training Strategy

####1. NAVIDA architecture has been used for my code

The NAVIDA architecture include 5 CNN layers, 4 fully connected layers.
the first 3 CNN layers use kernel 5*5, and the rest of 2 CNN layers use kernel 3*3.
the depths of CNN layers is from 24 ==>36==>48==>48==>64 
the 4 fully connected layers have the neurons from 1164 into 1 
the output layer is one, because it's differnt with traffic sign, the output is one for used steering angle.

####2. Attempts to reduce overfitting in the model

The model was trained and validated on different data sets to ensure that the model was not overfitting (0.2 of total sets is used for test, validation_split=0.2). 
Overfitting prevent: During the process, first before training the data, those data were shuffle, then i set the epoch=5, and find the loss and accuracy is is almost the same for the last 2 epochs, that's means it's overfitting, so i change epochs into 3 to prevent overfitting.
The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

####3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 25).

####4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. firstly, I used the center camera data to train my architure. 
At the last, i add the right/left side camera, flipped image as the challage training after this submittion (this time i havn't train it yet)

###Model Architecture and Training Strategy

####1. Solution Design Approach

The overall strategy for deriving a model architecture was to using the human driving data to train the net learn how to drive like human

The first step was to use a NAVIDA architure similar to the pipeline I thought this model might be appropriate because the NAVIDA is proved to be good for training self_driving vehcle to learn how to driving (input image, output steering angle) 

####2. model

The final model architecture  consisted of a convolution neural network with the following layers and layer sizes:
![image](https://github.com/Genzaiwuxian/term1-p3/blob/master/architecture.jpg)

####3. Creation of the Training Set & Training Process

To capture good driving behavior, I recorded one lap on track one using center lane driving. Here is an example image of center lane driving:
![image](https://github.com/Genzaiwuxian/term1-p3/blob/master/center_2017_11_05_21_49_42_498.jpg)

However i find the result doesn't work very well on the first curve, so i added some driving behavior in the corners, the images are like:
![image](https://github.com/Genzaiwuxian/term1-p3/blob/master/center_2017_11_05_21_49_10_477.jpg)
![image](https://github.com/Genzaiwuxian/term1-p3/blob/master/center_2017_11_05_21_49_57_311.jpg)
finally, i find the result is ok, so i didn't add the life/right images, but i add the code in my pipeline for runing left/right cameras, and left it after this project for Amason aws ec2 service

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle nearly fell off the track, so it's better input some more images in corners to train let again, to improve the driving behavior.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

the result of train:
## Epoch 1/3: loss: 81.0132 - val_loss: 0.0162
## Epoch 2/3: loss: 0.0141 - val_loss: 0.0138
## Epoch 3/3: loss: 0.0121 - val_loss: 0.0131

## shotage:
- vehicle do not turn very well in corners, it's better input more corners behavioral images
- i finishhed the net, adding "left/right cameras", and also adding "flipped images", it's the challange for me to train those images (it's too big and too much images, so i didn't train this time, maybe it's better use AWS EC2, this time i didn't use it, because the poor connection link with service)
