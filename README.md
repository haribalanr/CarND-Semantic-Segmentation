# Semantic Segmentation
### Introduction
This project, labels the pixels of a road in images using a Fully Convolutional Network (FCN) (Forked from https://github.com/udacity/CarND-Semantic-Segmentation)

Goal is to construct a fully convolutional neural network based on the VGG-16 image classifier architecture for performing semantic segmentation to identify drivable road area as seem from a car dashcam image. This project was trained and tested on the KITTI data set.

### Overview
A pre-trained VGG-16 network was loaded and made to a FCN by converting the final fully connected layer to a 1x1 convolution and setting the depth equal to the number of desired classes (i.e., road and not-road). 
Performance improvement was done by use of skip connections, performing 1x1 convolutions on previous VGG layers (here, layers 3 and 4) and adding them element-wise to upsampled (through transposed convolution) lower-level layers (i.e. 1x1-convolved layer 7 is upsampled before being added to the 1x1-convolved layer 4). Each convolution and transpose convolution layer includes a kernel initializer and regularizer

- Adam optimizer was used.
- Cross-entropy was the loss function for the network.

Hyperparameters used for training are:
keep_prob: 0.5, batch_size: 5, learning_rate: 0.0009, epochs: 50

Loss per batch averages below 0.200 after couple epochs and then below 0.100 after ten epochs. Average loss per batch at epoch 20: 0.057, at epoch 30: 0.075, at epoch 40: 0.035, and at epoch 50: 0.031

Over all performance was good, however there are roam for improvements as where few images have spotty raod identification. Playing more with Hyperparameters and faster training with Gpu can help as well (allowing more epochs).

### Image Sample output from FCN
Segmentation class overlaid in green over the upon the image.
![sample1](./images/uu_000004.png)
![sample2](./images/uu_000011.png)
![sample3](./images/uu_000022.png)
![sample4](./images/uu_000027.png)
![sample5](./images/uu_000034.png)
![sample6](./images/uu_000054.png)
![sample8](./images/uu_000064.png)
![sample7](./images/uu_000088.png)
![sample9](./images/uu_000094.png)
![sample10](./images/uu_000095.png)
![sample11](./images/uu_000098.png)



### Setup Information
##### Frameworks and Packages
Make sure you have the following is installed:
 - [Python 3](https://www.python.org/)
 - [TensorFlow](https://www.tensorflow.org/)
 - [NumPy](http://www.numpy.org/)
 - [SciPy](https://www.scipy.org/)
##### Dataset
Download the [Kitti Road dataset](http://www.cvlibs.net/datasets/kitti/eval_road.php) from [here](http://www.cvlibs.net/download.php?file=data_road.zip).  Extract the dataset in the `data` folder.  This will create the folder `data_road` with all the training a test images.

### Start
##### Implement
Implement the code in the `main.py` module indicated by the "TODO" comments.
The comments indicated with "OPTIONAL" tag are not required to complete.
##### Run
Run the following command to run the project:
```
python main.py
```
**Note** If running this in Jupyter Notebook system messages, such as those regarding test status, may appear in the terminal rather than the notebook.

### Submission
1. Ensure you've passed all the unit tests.
2. Ensure you pass all points on [the rubric](https://review.udacity.com/#!/rubrics/989/view).
3. Submit the following in a zip file.
 - `helper.py`
 - `main.py`
 - `project_tests.py`
 - Newest inference images from `runs` folder  (**all images from the most recent run**)
 
 ### Tips
- The link for the frozen `VGG16` model is hardcoded into `helper.py`.  The model can be found [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/vgg.zip)
- The model is not vanilla `VGG16`, but a fully convolutional version, which already contains the 1x1 convolutions to replace the fully connected layers. Please see this [forum post](https://discussions.udacity.com/t/here-is-some-advice-and-clarifications-about-the-semantic-segmentation-project/403100/8?u=subodh.malgonde) for more information.  A summary of additional points, follow. 
- The original FCN-8s was trained in stages. The authors later uploaded a version that was trained all at once to their GitHub repo.  The version in the GitHub repo has one important difference: The outputs of pooling layers 3 and 4 are scaled before they are fed into the 1x1 convolutions.  As a result, some students have found that the model learns much better with the scaling layers included. The model may not converge substantially faster, but may reach a higher IoU and accuracy. 
- When adding l2-regularization, setting a regularizer in the arguments of the `tf.layers` is not enough. Regularization loss terms must be manually added to your loss function. otherwise regularization is not implemented.
 
### Using GitHub and Creating Effective READMEs
If you are unfamiliar with GitHub , Udacity has a brief [GitHub tutorial](http://blog.udacity.com/2015/06/a-beginners-git-github-tutorial.html) to get you started. Udacity also provides a more detailed free [course on git and GitHub](https://www.udacity.com/course/how-to-use-git-and-github--ud775).

To learn about REAMDE files and Markdown, Udacity provides a free [course on READMEs](https://www.udacity.com/courses/ud777), as well. 

GitHub also provides a [tutorial](https://guides.github.com/features/mastering-markdown/) about creating Markdown files.
