# Automatic Gemstone Classification Using Computer Vision

Repository related to a manuscript currently under peer-review. Upon acceptance this Readme will be expanded to serve as a user manual.

<img src="Fig_1_montage.png" height="250" />


## Abstract

This paper presents a computer vision-based methodology for automatic image-based classification of 2042 training images and 284 unseen images divided into 68 categories of gemstones.
A series of feature extraction techniques (33 including colour histograms in RGB, HSV and CIELAB space, local binary pattern, Haralick texture and grey-level co-occurrence matrix properties) were used in combination with different machine learning algorithms (Logistic Regression, Linear Discriminant Analysis, K-Nearest Neighbour, Decision Tree, Random Forest, Naïve Bayes, Support Vector Machine). Deep learning classification with ResNet-18 and ResNet-50 was also investigated. 
The optimal combination was provided by a Random Forest algorithm and RGB 8-bin colour histogram and local binary pattern features, with an accuracy of  69.4\% on unseen images within only 0.0165 second to process. The robustness of the system was verified by comparing against than three experts gemmologists having at least 5 years of experience in gemstone identification (accuracy was 42.6--66.9\% within 42--175 minutes). Although these results were obtained in a relatively low number of images, the superiority of the computer vision over humans is inline with what has been reported in other areas of study.




<img src="Fig_5_RGB.png" height="200" /> <img src="Fig_5_HSV.png" height="200" /> <img src="Fig_5_LAB.png" height="200" />

