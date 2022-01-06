# Automatic Gemstone Classification Using Computer Vision

Repository related to the manuscript "Automatic Gemstone Classification Using Computer Vision" by Bona Hiu Yan Chow and Constantino Carlos Reyes-Aldasoro published in the Minerals MDPI journal, 2022, 12(1), 60 (doi: 10.3390/min12010060). 

Full-text PDF: https://www.mdpi.com/2075-163X/12/1/60/pdf

<img src="Fig_1_montage.png" height="250" />


## Abstract


This paper presents a computer-vision-based methodology for automatic image-based classification of 2042 training images and 284 unseen (test) images divided into 68 categories of gemstones. A series of feature extraction techniques (33 including colour histograms in the RGB, HSV and CIELAB space, local binary pattern, Haralick texture and grey-level co-occurrence matrix properties) were used in combination with different machine-learning algorithms (Logistic Regression, Linear Discriminant Analysis, K-Nearest Neighbour, Decision Tree, Random Forest, Naive Bayes and Support Vector Machine). Deep-learning classification with ResNet-18 and ResNet-50 was also investigated. The optimal combination was provided by a Random Forest algorithm with the RGB eight-bin colour histogram and local binary pattern features, with an accuracy of 69.4% on unseen images; the algorithms required 0.0165 s to process the 284 test images. These results were compared against three expert gemmologists with at least 5 years of experience in gemstone identification, who obtained accuracies between 42.6% and 66.9% and took 42–175 min to classify the test images. As expected, the human experts took much longer than the computer vision algorithms, which in addition provided, albeit marginal, higher accuracy. Although these experiments included a relatively low number of images, the superiority of computer vision over humans is in line with what has been reported in other areas of study, and it is encouraging to further explore the application in gemmology and related areas.


<img src="Fig_5_RGB.png" height="200" /> <img src="Fig_5_HSV.png" height="200" /> <img src="Fig_5_LAB.png" height="200" />


## Dataset


A total of 2326 images of gemstones were obtained from [Kaggle](https://www.kaggle.com/lsind18/gemstones-images) (accessed on 27 April 2021) and analysed in this work. The images were grouped into categories, and for this work the following 68 classes were selected for analysis: *Alexandrite, Almandine, Amazonite, Amber, Amethyst, Ametrine, Andradite, Aquamarine, Aventurine Green, Aventurine Yellow, Benitoite, Beryl Golden, Bixbite, Bloodstone, Blue Lace Agate, Carnelian, Chalcedony, Chalcedony Blue, Chrome Diopside, Chrysoberyl, Chrysocolla, Chrysoprase, Citrine, Coral, Diamond, Diaspore, Dumortierite, Emerald, Fluorite, Hessonite, Iolite, Jasper, Kunzite, Kyanite, Lapis Lazuli, Malachite, Onyx Black, Onyx Green, Onyx Red, Peridot, Prehnite, Pyrite, Pyrope, Quartz Beer, Quartz Lemon, Quartz Rutilated, Quartz Smoky, Rhodochrosite, Rhodolite, Rhodonite, Ruby, Sapphire Blue, Sapphire Pink, Sapphire Purple, Sapphire Yellow, Serpentine, Sodalite, Spessartite, Sphene, Sunstone, Tanzanite, Tigers Eye, Topaz, Tourmaline, Tsavorite, Turquoise, Zircon* and *Zoisite*. A total of 2042 images were used for training %the computer vision systems and 284 images were reserved for testing. For each class, 24--44 training images and 4--5 test images were available.

The original Kaggle dataset consists of 2856 images distributed in 87 classes, but some of these were discarded according to the following criteria.
* The category *Garnet* was removed due to overlapping with *Almandine*, *Pyrope*, *Rhodolite* and *Spessartine*.
* The *Moonstone* images displayed a variety of either orange, white or yellow colour, which was undesirable for the algorithms, and were thus eliminated. 
* Upon background segmentation, poorly segmented training images satisfying either of these conditions were discarded: (1) incomplete removal of background, or (2) extraction of only a minor portion of gemstone. Seventeen classes, namely *Andalusite*, *Cats Eye*, *Danburite*, *Goshenite*, *Grossular*, *Hiddenite*, *Jade*, *Labradorite*, *Larimar*, *Morganite*, *Opal*, *Pearl*, *Quartz Rose*, *Scapolite*, *Spinel*, *Spodumene* and *Variscite*, were removed, as fewer than 24 training images per class were retained.

* *[test_masked](./test_masked)* contains the masked test images.
* *[test_selected](./test_selected)* contains the selected test images.
* *[train_masked](./train_masked)* contains the masked training images.
* *[train_selected](./train_selected)* contains the selected training images.



## Code files


All the algorithms used in this work were coded in Python 3.7.9. 


**Data Exploration and Pre-processing**

* *[InspectImages](./InspectImages.ipynb)* contains an initial inspection of the image dataset.


**Background Segmentation**

We applied Otsu thresholding based on grey-level intensity or the Saturation channel of HSV colour space to automatically extract the gemstones from the backgrounds.

* *[BackgroundSegmentationExperiment_Intensity.ipynb](./BackgroundSegmentationExecution.ipynb)* includes an exploration of intensity-based Otsu thresholding using the training images.
* *[BackgroundSegmentationExperiment_Saturation.ipynb](./BackgroundSegmentationExperiment_Saturation.ipynb)* includes an exploration of saturation-based Otsu thresholding using the training images.
* *[BackgroundSegmentationExecution.ipynb](./BackgroundSegmentationExperiment_Saturation.ipynb)* includes background segmentation of the entire image dataset using the best approach determined with the training images.


**Feature and algorithm comparison**

Seven different machine-learning algorithms (Logistic Regression, Linear Discriminant Analysis, K-Nearest Neighbour, Decision Tree, Random Forest, Naïve Bayes and Support Vector Machine) were compared, each with 33 different feature extraction methodologies (including colour histograms, local binary pattern, Haralick texture and grey-level co-occurrence matrix properties), which provided a total of $ 7 \times 33 = 231$ combinations. Deep-learning classification (transfer learning) with ResNet-18 and ResNet-50 was also investigated. With the exception of transfer learning, the scripts were executed on a MacBook Pro equipped with a 2.3 GHz Intel Core i5 processor. Transfer learning was implemented on a virtual NVIDIA Tesla K80 Graphics Processing Unit (GPU) with two workers in Google Colaboratory. 

* *[KMeans-CIELAB.ipynb](./KMeans-CIELAB.ipynb)* includes the extraction of CIELAB colour of the non-background K-means cluster centre.
* *[KMeans-HSV.ipynb](./KMeans-HSV.ipynb)* includes the extraction of HSV colour of the non-background K-means cluster centre.
* *[KMeans-RGB.ipynb](./KMeans-RGB.ipynb)* includes the extraction of RGB colour of the non-background K-means cluster centre.
* *[MachineLearning.ipynb](./MachineLearning.ipynb)* contains the extraction of all features except K-means clustering, as well as the training and evaluation of machine learning algorithms. 
* *[resnet.ipynb](./resnet.ipynb)* contains the implementation of transfer learning with ResNet-18 and ResNet-50.


**Predictions by Expert Gemmologists**

The expert group consisted of three gemmologists with both Graduate Gemologist of Gemological Institute of America (GIA) and Fellowship of the Gemmological Association of Great Britain qualifications and 5--8 years of experience in gemstone identification. The predictions of the test images made by each gemmologist are available in *[predictions1.csv](./predictions1.csv)*, *[predictions2.csv](./predictions2.csv)* and *[predictions3.csv](./predictions3.csv)*.

* *[HumanVision.ipynb](./HumanVision.ipynb)* contains an analysis of each gemmologist's predictions.


**Visualisations** 

Experimental findings were visualised using Python and Tableau. All figures used in the paper can be downloaded from the subfolder 'figures'.

* *[Figure_1_montage.ipynb](./Figure_1_montage.ipynb)* contains the Python codes for creating [Figure 1](./figures/Fig_1_montage.png) a montage of 500 gemstone images.
* *[BackgroundSegmentationExperiment_Intensity.ipynb](./BackgroundSegmentationExperiment_Intensity.ipynb)* and *[BackgroundSegmentationExperiment_Saturation.ipynb](./BackgroundSegmentationExperiment_Saturation.ipynb)* contain the Python codes for generating the binary masks in [Figure 4(b)](./figures/Fig_4_alexandrite_grey.png), [Figure 4(c)](./figures/Fig_4_alexandrite_saturation.png), [Figure 4(e)](./figures/Fig_4_amazonite_grey.png), [Figure 4(f)](./figures/Fig_4_amazonite_saturation.png), and the masked image of *Alexandrite* in [Figure 7(a)](Fig_7_masked.png).
* *[Figure_5_scatterplots.ipynb](./Figure_5_scatterplots.ipynb)* includes the Python codes for creating the scatter plots in [Figure 5(a)](./figures/Fig_5_RGB.png) RGB, [Figure 5(b)](./figures/Fig_5_HSV.png) HSV and [Figure 5(c)](./figures/Fig_5_LAB.png) CIELAB space.
* *[Figures_6_7.ipynb](./Figures_6_7.ipynb)* contains the Python codes for creating [Figure 6](./figures/Fig_6_HSVplots.png) polar scatter plot in HSV space, [Figure 7(b)](./figures/Fig_7_RGBscatterplot.png) scatter plot of RGB values of all pixels in an image of *Alexandrite*, [Figure 7(e)](./figures/Fig_7_RGBhistogram.png) RGB histogram, [Figure 7(f)](./figures/Fig_7_HSVhistogram.png) HSV histogram and [Figure 7(g)](./figures/Fig_7_LABhistogram.png) CIELAB histogram.
* *[KMeans-RGB.ipynb](./KMeans-RGB.ipynb)* included the Python codes for producing the RGB colour of the non-background K-means cluster of the masked image of *Alexandrite* in [Figure 7(c)](./figures/Fig_7_RGBkmeans.png).
* *MachineLearning.ipynb* contains the Python codes for generating the grey-level co-occurrence matrix in [Figure 7(d)](./figures/Fig_7_GLCM.png), the local binary pattern histogram in [Figure 7(h)](./figures/Fig_7_LBP.png) and the confusion matrix for the best algorithm in [Figure 9](./figures/Fig_9_bestsystem.png).
* *[Figure_8_results_boxplot.twb](./Figure_8_results_boxplot.twb)* includes the Tableau file used to create [Figure 8](./figures/Fig_8_accuracy) the box plot showing the results for all combinations of machine learning algorithms and feature extraction methodologies aggregated by algorithm.
* *[HumanVision.ipynb](./HumanVision.ipynb)* contains the Python codes for producing the confusion matrix of the best gemmologist in [Figure 10](./figures/Fig_10_bestexpert.png).


## Citation


If you find our work useful, please cite us as:

Chow, B.H.Y.; Reyes-Aldasoro, C.C. Automatic Gemstone Classification Using Computer Vision. Minerals 2022, 12, 60. https://doi.org/10.3390/min12010060

Chow BHY, Reyes-Aldasoro CC. Automatic Gemstone Classification Using Computer Vision. Minerals. 2022; 12(1):60. https://doi.org/10.3390/min12010060

Chow, Bona H.Y., and Constantino C. Reyes-Aldasoro. 2022. "Automatic Gemstone Classification Using Computer Vision" Minerals 12, no. 1: 60. https://doi.org/10.3390/min12010060




