[//]: # (Image References)

[image1]: ./examples/kitti.png



# Vehicle Detection using Linear SVM Classifier
The Project
---
Here, we are going to explain the steps to install/run the package and the main additions/modifications to the source package listed in credits.


#### **Credits**
This project is based on ajsmilutin's modification of the Udacity project https://github.com/ajsmilutin/CarND-Vehicle-Detection
---

## Package installation requirements
* Python 3.6.5
* OpenCV 3.4.1
* Scipy 1.1.0
* Numpy 1.14.3
* Other Libraries needed :
  - Scikit-learn 0.19.1 (Python library for machine learning)
  - Standardizing features by removing the mean and scaling to unit variance (using the class StandardScaler with its functions fit() and transform())
  - Splitting arrays or matrices into random train and test subsets (using the class model_selection with the splitter function train_test_split)
  - Implementing the Linear Support Vector Classification (instantiating the object with LinearSVC and using the functions fit(), predict() and score() )
Matplotlib 2.2.2 (Python library for 2D plotting)
Moviepy 0.2.3.4 (Python library for video editing)
Scikit-image 0.13.1 (Python library for image processing)
Used for the Histogram of Oriented Gradients

