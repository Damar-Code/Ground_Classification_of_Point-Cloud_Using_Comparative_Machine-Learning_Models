# Ground_Classification_of_Point-Cloud_Using_Comparative_Machine-Learning_Models

Ground Classification is fundamental step for impelementing LiDAR in Forest Inventory Purposes to understand the tree structural properties. In "lidR" package it self already provided model for classify ground point, such as: Progressive Morphological Filter (PMF), Cloth Simulation Function (CSF) and Multiscale Curvature Classification (MCC). However, all those models are still not accurate anough for landscape scale, especially for areas with complex terrain. On another hand, those algorithms take an extremely long time of processing for landscape scale. Therefore, be needed Machine Learning for building highly accurate ground classification models, but did not take much processing time.

## METHODE
Builing Ground Classification model in this study are using 19 predictors. There are 6 predictors originally from LiDAR it self, such as intensity, R, G, B, NIR, and scan angle. Moreover, to understand the terrain complexity there are additional geometrical features as the predictors, such as Zmin, slope, index, planar, 1st eigenvalue, 2nd eigenvalue, 3rd eigenvalue, sum Eigen, anisotropy, planarity, linearity, SV, and Sphericity.

In order to obtain robust models, there is a comparison of five models, which is C5.0, GBM, SVM, KNN, and Ensemble. There are around 200,000 point cloud as a dataset, which is 70% for training and 30% for testing. Meanwhile, in the validation phase, there are two steps: first, validation using a testing dataset and second, revalidating the models in landscape scale using actual ground dataset.

![Flow Chart_Ground Classification](https://user-images.githubusercontent.com/60123331/211615140-18bb2de3-67f4-4409-9509-a17b6647db22.png)

Figure 1. Workflow of Building Ground Classification Model Using Machine Learning

Area of Intesest as a training dataset to build machine learning models in this study showed in this picture below. The terrain condition is quite hilly with dense forest canopy. 

![AoI](https://user-images.githubusercontent.com/60123331/211566665-75e690dc-13cf-4871-ae6f-11b3aaeb7f7e.png)

Figure 2. Area of Interest as a Training Dataset

### Feature Selection
Feature selection in sthis study using two steps, Correlation Metrics and Recursive Feature Elimination. Correlation Metrics is usefull to avoid the multicollinearity from the predictors. Using cut-off 0.7 eliminated index, planar, SV, 2nd eigenvalue, 3rd eigenvalue, and sum eigenvalue.

![Corrpot - Resize](https://user-images.githubusercontent.com/60123331/211583983-48c0f339-4d69-4ec8-a58e-a5c21b3ec6d2.png)

Figure 3. Correlation Metrics

Following the removal of predictors with high correlation,  the rest of the predictors are pitted to find the most significant predictors. Figure 4 below shows there are six important variables to classify ground point cloud, there are sphericity, 1st eigenvalue, intensity, linearity, planarity, and index.

![Variable Importance - resize](https://user-images.githubusercontent.com/60123331/211583792-cb679b55-becb-4fa5-8971-2f16f897e3f2.png)

Figure 4. Variable Importance

## RESULT AND DISCUSSION

![model_comparison - resize](https://user-images.githubusercontent.com/60123331/211583738-396298ab-22b7-4fe9-85da-363450b5173c.png)

Figure 5. Accuracy and Kappa
Clearly see that how the algorithms performed in terms of accuracy and kappa. The C5.0 model appears to be the be best performing model overall because of the high accuracy and Kappa. Either way, there are second validation to make final decision on which model will have best peformance.



## Second Validation

Second validation done by MAPE analysis of model impelementation in new dataset with the bigger area scale. Cross section below shows how the model classified the ground and nonground point cloud. Mostly the model are underestimated which mean some point cloud that should be classify as a ground, instead a be non ground. Root cause of that underestimating might derive by the distribution of the number of ground point cloud are way less than the nonground point cloud (vegetation). Usually forest area will lacking of ground point cloud becasue the point cloud cannot penetrate untill touch the ground because of the canopy.

![cross section map](https://user-images.githubusercontent.com/60123331/211581039-c105c088-d344-4932-a4ea-5d374087222f.png)

MAPE value from each model are got from its differences value between the actual ground data. It means the differences between elevation value. Sampling point distribution for MAPE analysis are using purposive sampling technique, focused on abnormality area with some outlier are there. The outliers it self are clearly visible from the Digital Elevation Model Map below

![Sampling MAPE - Copy](https://user-images.githubusercontent.com/60123331/211584330-85584766-20e6-4519-bf7c-6542a35fc51b.png)

Each models performance clearly seen from the digital elevation model below. 


![comparison](https://user-images.githubusercontent.com/60123331/211609241-108e1a09-03a0-4135-9691-6cbf43574c33.png)


![MAPE](https://user-images.githubusercontent.com/60123331/211611038-a7ab234e-dffc-4b08-bbca-967d906473a1.png)



## CONCLUSION

