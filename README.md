# Change Detection
### Abstract
The project aims to find and show the changes of two images. For example, by taking satellite images at two different times of the same place, 
the program can detect new roads, buildings, etc. 
After many trials, we decided to use Unet CNN with VGG16 encoder for training. 
Unet is known as one of the successful model architectures for image segmentation. It performed the best showing [iou score] IOU score. 

### Data Loader
The model is fed in this way: the data loader reads images from a directory, creates batches,
passes them through augmentation techniques, then concatenates 'before' and 'after' images of the same place and with the mask of the image gives to the model.

### Data
The augmentation layers contain dozens of combinations and techniques like flipping, bending, cropping, padding, color changing, etc.
Besides the augmentation techniques, two methods for new data creation were made. 
The first one creates new realistic images by extracting objects from some images and using OpenCV seamless cloning pastes them on a new background. And the second one is for creating a synthetic dataset from geometric shapes. 
Via the new datasets, the accuracy of the model has significantly increased. 

### Performance
The performance of the model was tracked by IoU score(also known as Jaccard's index), F1 score, and of course visualization by tensorboard. 
The IoU is the area of overlap between the predicted segmentation and the ground truth divided by the area of union between the predicted segmentation and the ground truth. 
The F1 score is the combination of precision and recall.  Tensorboard is a visualization tool. 
As the loss function, the binary focal dice loss was used. It's able to reduce the contribution from easy images and make the model focus on hard examples. 
