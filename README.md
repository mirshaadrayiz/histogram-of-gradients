# histogram-of-gradients

Histogram of Gradients for Feature Extraction

BASED ON - HOG Method proposed by Dalal & Triggs in their paper "Histograms of Oriented Gradients for Human Detection, CVPR, 2005".

CONCEPT - Gradient orientations in the edges of an object in an image will have a noteworthy difference from the gradients in the other flat regions. Using this difference, the edges can be detected to seperately identify an object from its background. 

Programming Languages Used - PYTHON
Libraries  - OpenCV, Numpy, Matplotlib


### INSTALLATIONS REQUIRED

1. Python : https://www.python.org/downloads/
2. OpenCV : https://pypi.org/project/opencv-python/
3. Numpy  : https://docs.scipy.org/doc/numpy-1.10.1/user/install.html
4. matplotlib : https://matplotlib.org/faq/installing_faq.html


## The HOG Algorithm


#### Initializing the cell structure

First, we initialize the data structure (cell_gradient_vector) that will be used to store the gradient information.

The input image is divided into smaller cells with each bin to be processed seperately. The parameters `cell_size`,`height` & `width` determine the number of cells. 

As we compute gradient orientations in the images, the orientations must be quantized. The `angle_unit` parameter specifies the angle (in degrees) that defines the size of each bin in the histogram. For e.g., if `angle_unit` is set to 20, number of bins would be **180/20 = 9**.The way this works is, if a gadient angle of 45 and magnitude 10 is encountered, a value of 10 will be added to the 2nd bin.

Using the above parameters, the `cell_gradient_vector` that will be used to store the gradients is defined.



#### HOG Computation

When an image is obtained as an input, The `def_gradient()` function is called and it computes the gradients in the *x directions* and *y directions* seperately using `cv2.sobel()` function. The result is used to compute the **Gradient Magnitude** and the **Gradient Angle** for the whole image. Then the corresponding sub regions of the gradient angle and gradient magnitude for each cell is obtained by iterating through each cell using the pre-initialized `cell_gradient_vector`. These magnitude and angle values for each cell are stored in variables `cell_magnitude` and `cell_angle` and passed onto the function `cell_gradient`. The `cell_gradient` function iterates through every pixel in the cell and computes the gradient orientation (gradient strength ***g<sub>x</sub>*** and gradient angle ***g<sub>y</sub>***) for each pixel using the magnitude and angle values. 

![image](https://github.com/mirshaadrayiz/histogram-of-gradients/assets/147004775/272af5b2-3d14-4c6c-8d7d-1b90a003c570)


The appropriate bin for this **gradient angle** is identified (depends on pre-initialized **angle_unit** value) and the **gradient_strength** value is added to that bin. By doing this for each pixel, a histogram of gradients is formed. The histogram is also plotted using `matplotlib` for visualization.

The above process is repeated for each cell which results in a filled `cell_gradient_vector`. This is followed by the formation of 2x2 blocks by combining neighbouring cells. For each block, the **gradient oreintations** of the cells are concatanated forming **block vectors**. These block vectors together form the hog vector which is our final feature vector. This vector can now be used as a feature vector to extract features from images. 

## TESING THE ALGORITHM

car.jpg has been used to test the implementation.

##### Feature vector output for the test data

![image](https://github.com/mirshaadrayiz/histogram-of-gradients/assets/147004775/e65c1a66-00d1-46e4-9ce6-c5b2baea05b1)

##### Visualization of the Histogram of Gradients for a single cell

![image](https://github.com/mirshaadrayiz/histogram-of-gradients/assets/147004775/a111a7e9-471a-43b6-8c92-dd6897270044)
