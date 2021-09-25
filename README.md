# Deep Learning

## Charity Funding Predictor



### Overview

The purpose of this analysis is to create a deep learning model with various layers and neurons to predict if a charity will receive funding. This uses a dataset with several features.



### Results

#### Data Preprocessing

During data preprocessing, a number of steps are taken to prepare the data for the neural network:

- The target variable for the model is "IS_SUCCESSFUL". This is a binary showing 1 for successful or 0 for unsuccessful. This feature will be split out later.
- The variables that are neither targets nor features are "EIN" and "NAME". These features are dropped.
- All other variables are considered features for the neural network, as they have a basis on the outcome.
- Bins are created for "APPLICATION_TYPE" and "CLASSIFICATION" as they both have a small number of outliers.
- "Get Dummies" is used to convert the text-based features into binary.
- Now the data is split into features (X) and targets (y) and into training and testing sets using train test split.
- Finally, the data is scaled using Standard Scaler.



#### Compiling, Training, and Evaluating the Model

##### Run 1

I start with two hidden layers and a large number of neurons (80 first layer, 30 second), because I believe that a complicated model might get me to the target of 0.75 the quickest. This turns out to be false, as it had my lowest accuracy of 0.734. 

##### Run 2

Looking at the nunique of the data, I see that the ask amount "ASK_AMT" has a large number of unique values, so I make a box plot of that data:

<img src="https://github.com/adamholcomb/Deep-Learning/blob/main/Resources/image-20210925145919964.png" alt="image-20210925145919964" style="zoom: 80%;" /> <img src="https://github.com/adamholcomb/Deep-Learning/blob/main/Resources/image-20210925150113197.png" alt="image-20210925150113197" style="zoom: 80%;" />

This shows such a wide range of outliers, so I look at the lower and upper bounds of the box plot using the quartiles plus and minus 1.5 * interquartile range. This gives outlier cutoffs of 887 and 11,855. Removing these outliers and running the neural network with the same number of nodes as above results in a higher accuracy: 0.744. This is still under the target, but better than Run 1.

##### Run 3

For Run 3 I adjust the model parameters to attempt a higher accuracy. This time I reduce the number of nodes from 80 to 30 in layer one. I also change the activation in layer two from relu to tanh. The epochs are also increased from 50 to 75. These changes have very little impact on the overall accuracy, which stays at 0.744, about equal to Run 2. 



### Summary: 

Run 1 has an overcomplicated neural network and a dataset with many outliers. Removing the outliers for Run 2 increases the accuracy substantially from 0.734 to 0.744. However, changing parameters of the neural network and making it less complicated has little impact on the accuracy, which remains at 0.744. This shows that the model is complicated enough, and either decreasing nodes/layers or changing the number/makeup of features would more greatly increase accuracy. The models are close, however, and individual testing runs are above 0.75. The accuracy plot of Run 3 shows this as well:

![image-20210925151724935](https://github.com/adamholcomb/Deep-Learning/blob/main/Resources/image-20210925151724935.png)

