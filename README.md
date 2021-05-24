# Custom-Haar-cascade-Mask-Classifier

Custom haar cascade classifier created to detect face with and without face masks

The custom haarcascade xml file is trained using the Cascade Trainer GUI tool provided in the following link:  https://amin-ahmadi.com/cascade-trainer-gui/

/classifier folder consists of the stage-by-stage xml files generated during the model training.

/classifier/cascade.xml is the final xml file after training the model with face images with and without masks. 


# Installation

Currently Cascade Trainer GUI can be used on Windows (7 or above) and Linux using Wine. The installation procedure is pretty straightforward and it only involves pressing a couple of “Next” buttons. Click on the below link to download the Cascade trainer GUI.

Windows x64

https://amin-ahmadi.com/downloadfiles/cascadetrainergui/CascadeTrainerGUI_3.3.1_x64_Setup.exe

Windows x86

https://amin-ahmadi.com/downloadfiles/cascadetrainergui/CascadeTrainerGUI_3.3.1_x86_Setup.exe

#### **NOTE** 

x64 version is recommended for the 64-bit systems

To train classifiers usually you need to provide the utility with thousands of positive and negative image samples, but there are cases when you can achieve the same with less samples.

To start the training, you need to create a folder for your classifier. Create two folders inside it. One should be “p” (for positive images) and the other should be “n” (for negative images).

Positive image samples are the images of the object you want to train your classifier and detect. Negative images are anything other than the positive images. (Adding grayscale images for positives will increase accuracy)

For example, we are training a custom classifier to detect people faces w/ and w/o face masks, positive images will consists of people faces w/ and w/o masks and negative folder will consists of images of anything other than people.

![GitHub Logo](/images/images_Pos_Neg.png) 

#### **NOTE**

Important Note 1: Negative images must NEVER include any positive images. Not even partially.

Important Note 2: In theory, negative images can be any image that is not the positive image but in practice, negative images should be relevant to the positive images. For example, using sky images as negative images is a poor choice for training a good car classifier, even though it doesn’t have a bad effect on the overall accuracy:

# Training Process

:point_right: Step 1

Start by pressing the Browse button in Train tab. Select the folder you have created for the classifier. The positive images usage(percentage) must be set to 90% of the total images in the p folder so that the training doesn't end up in errors like below:
"OpenCV Error : Bad argument(Can not get new positive sample.The most possible reason is insufficient count of samples in given vec - file.) in CvCascadeImageReader::PosReader::get, file \path_to_opencv\apps\traincascade\imagestorage.cpp, line X"

Checkout this page if any error arises during the training process : http://amin-ahmadi.com/2017/07/26/how-to-get-past-the-infamous-insufficient-count-of-samples-error-in-opencv-cascade-training/
Set the negative image count to the number of negative images in the n folder.

Cascade Trainer GUI sets the most optimized and recommended settings for these parameters by default, still some parameters need to be modified for each training. Note that detailed description of all these parameters are beyond the scope of this help page and require deep knowledge about cascade classification techniques.

:point_right: Step 2

You can set pre-calculation buffer size to help with the speed of training process. You can assign as much memory as you can for these but be careful to not assign too much or too low. For example if you have 8 GB of RAM on your computer then you can safely set both of the buffer sizes below to 2048. You can also adjust the number of stages according to the training needs and accuracy.
 

:point_right: Step 3

Next you need to set the sample width and height. Make sure not to set it to a very big size because it will make your detection very slow. Actually it is quite safe to always set a small value for this. Recommended settings for sample width and height is that you keep one aspect on 24 and set the other accordingly.


:point_right: Step 4

As for the parameters in the Boost tab, it is recommended to keep the default values unless you are quite sure about what you’re doing.


After all the parameters are set, press Start button at the bottom to start training your cascade classifier. You’ll see the following log screen while training is going on. Wait for the training to complete. You will get a dialog box stating that the training is complete.



Now if you exit Cascade Trainer GUI and go to the classifier folder you will notice that there are new files and folders are created in this folder.

“n” and “p” are familiar but the rest are new. “classifier” folder contains XML files that are created during different stages of training. If you check inside “classifier” folder, you’ll notice something similar to the following.

“stage#.xml” files are temporary files that won’t be needed anymore.

“params.xml” contains the parameters you have used for the training. (Just a reminder file)

“cascade.xml” is the actual cascade classifier and if the training completed successfully then you should have this file inside classifier folder.

“neg.lst”, “pos.lst” and “pos_samples.vec” are temporary files created for training the classifier and they can also be removed without having any effect.



