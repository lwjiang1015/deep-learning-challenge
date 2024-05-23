# deep-learning-

## Overview of the Analysis

This project attempts to generate a model, by building a neural networks, that help the nonprofit foundation Alphabet Soup select the applicants for funding with the best chance of success in their ventures, using the historical data. 

Firstly, the columns in the original dataset are separated into labels (y, the target) and features (both as mentioned above).   Two categorical features with too many classifications (APPLICATION_TYPE and CLASSIFICATION) are reduced to smaller set to reduce the number of features for quantatitive analyses. The data is then split into training and testing sub-datasets respectively with 25724 samples (75%) in the training dataset and 8575 samples (25%) in the testing dataset, out of the 34299 samples in the original datasets. A model, built via the neural networks, is then compiled, train, and evaluated before being exported as an HDF5 file. 

## Results

* Data Preprocessing:
    * The target is a binary classifier that can predict whether applicants will be successful if funded by Alphabet Soup, which equals to 1 if the money is to be used effectiely and 0 otherwise. 
    * The features that are used to predict the outcome are primarily categorical, including APPLICATION_TYPE, AFFLIATION for affiliated sector of industry, CLASSIFICATION for government organisation classification, USE_CASE for funding purpose, ORGANIZATION for organisation type, STATUS indicts whether it is active or not, INCOME_AMT are different ranges of income, SPECIAL_CONSIDERATIONS indicates whether there are special considerations for applicatoin (either YES or NO). The only non-categorical feature is ASK_AMT which is funding amount requested.
    * Two identification columns EIN and NAME are removed from the input data because they are neither targets nor features.

* Compiling, Training, Optimizing, and Evaluating the Model:
    * Originally, three layers are used for the neural network model given the small datasets but relatively large number of features. The neurons for the input layers are set as the same as the number of input features, following the niche, and activation functions used for the input layer and the first hidden layer are Rectified Linear Unit (relu) given its computationally efficiency and the small data size while a sigmoid activation is used for the output layer given the target being a binary classification. The number of neurons for the first hidden layer is set as 16 also due to the small data size. 
    * To optimize the model performace, the followings have been attempted: 
    (1) winsorised the only non-categorical feature ASK_AMT (the amount of money requested) and used the winsorised feature in the model;
    (2) removed the dummy feature "SPECIAL_CONSIDERATIONS_N" given it is the opposite to the dummy feature "SPECIAL_CONSIDERATIONS_Y".
    (3) with respect to model building, the following changes have been made sequentially to see which change may improve the model performace: (a) added one more hidden layer also with the activation function "relu" and with more (16) neurons, resulting increased accuracy from 0.7287 to 0.7292 but increased loss as well from 0.5564 to 0.5613. (b)the activation function "tanh" replaced "relu" in the first hidden layer, resulting in the descrease in both accuracy (from 0.7287 to 0.7268) and loss (from 0.5564 to 0.5530). Therefore, a decision is made that "relu" will be used as the activition function. (c) increased the epochs from 50 to 80 (smaller epochs are used given the small data size albeit larger feature sets), surprisingly the accuracy rate decreased (from 0.7287 to 0.7280) although loss also decreased (from 0.5564 to 0.5548). (d) finally, reduced the batch size from 32 to 25, the accuracy rate decreased from 0.7287 to 0.7252 and loss increased from 0.5564 to 0.5580; therefore the batch size revised back to 32. Therefore, the final decision was made to add more hidden layer and more neurons.
    * Even the final adjustments did not however succeed in improving the model performance to the desired level.
    
## Summary

In summary, the overall results show that the model developed/optimised could predict whether the funding will be successful with roughly 73% accuracy rate while more accurate predictions may be achieved with more exploration into the parameters used.  

Recommendation: in addition to further exploration into the modelling paramters and techiques, perhaps more quantitative data may be collected upon the application to be used for the model optimization and thereof more accurate predictions as to the effective usage of the funding in the future. 

## References and acknowledgements

- University of Adelaide. (2023). Module 20 contents in particular.
https://bootcampspot.instructure.com/courses/4781/pages/21-deep-learning?module_item_id=1163546
- The help from the teaching team, the Xpert Learning Assistant is acknowledged as usual.


**Data**
- Data for this dataset was generated by edX Boot Camps LLC, and is intended for educational purposes only.