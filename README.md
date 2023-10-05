# histogram-of-gradients

Histogram of Gradients for Vehicle Detection

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

As we compute gradient orientations in the images, the orientations must be quantized. The `angle_unit` parameter specifies the angle (in degrees) that defines the size of each bin in the histogram. For e.g., if `angle_unit` is set to 20, number of bins would be **180/20 = 9**. The height and weight

Using the above parameters, the `cell_gradient_vector` that will be used to store the gradients is defined.



#### Gradient Computation Concept

The `def_gradient()` function computes the gradient in the *x directions* and *y directions* seperately and then uses that to compute the Gradient Magnitude and the Gradient Angle. 

