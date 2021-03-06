# Change Detection
### Abstract
The project aims to find and show the changes of two images. For example, by taking satellite images at two different times of the same place, 
the program can detect new roads, buildings, etc. 

![A](https://github.com/Dav00Arm/Change_Detection_Post/blob/main/images/A2.jpg)
![B](https://github.com/Dav00Arm/Change_Detection_Post/blob/main/images/B2.jpg)
![OUT](https://github.com/Dav00Arm/Change_Detection_Post/blob/main/images/OUT2.jpg)


### Model
Model architecture is Unet convolutional neural network with VGG16 encoder. 
Unet is known as one of the successful model architectures for image segmentation.
This architecture performed the best result after many trials showing [IoU score] IoU score. 
Currently, works are going on the creation of a Siamese Network.
A Siamese neural network (sometimes called a twin neural network) is an artificial neural network that uses the same weights while working in tandem on two different input vectors to compute comparable output vectors.
![architecture](https://github.com/Dav00Arm/Change_Detection_Post/blob/main/images/model.png)


### Data Loader
The model is fed in this way: the data loader reads images from a directory, creates batches,
passes them through augmentation techniques, then concatenates 'before' and 'after' images of the same place and with the mask of the image gives to the model.

### Data
The augmentation layers contain dozens of combinations and techniques like flipping, bending, cropping, padding, color changing, etc.
Besides the augmentation techniques, two methods for new data creation were made. 
The first one creates new realistic images by extracting objects from some images and using OpenCV seamless cloning pastes them on a new background. And the second one is for creating a synthetic dataset from geometric shapes. 
Via the new datasets, the accuracy of the model has significantly increased. 

Custom synthetic and realistic data example:

![syn](https://github.com/Dav00Arm/Change_Detection_Post/blob/main/images/syn1.jpg)
![real](https://github.com/Dav00Arm/Change_Detection_Post/blob/main/images/14_3.jpg)

### Performance
The performance of the model was tracked by IoU score(also known as Jaccard's index), F1 score, and of course visualization by tensorboard. 
The IoU is the area of overlap between the predicted segmentation and the ground truth divided by the area of union between the predicted segmentation and the ground truth. 
The F1 score is the combination of precision and recall.  Tensorboard is a visualization tool. 
As the loss function, the binary focal dice loss was used. It's able to reduce the contribution from easy images and make the model focus on hard examples. 
