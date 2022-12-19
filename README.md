# phase3_project

## Description
  To build a model to that can predict the condition of a waterpump based on certain inout parameters
  
## Dataset
  Dataset sourced from https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/23/
  
## Methodololgy
  Since this a classifiaction problem, baseline models were built using Logistic Regression, Decision Trees and K-Nearest Neigbors.
  Out the of the three base models, the model with the best scores was chosen for further optimization
  
 ## Test Scores of baseline models
  ### Logistic Regression
  ![image](https://user-images.githubusercontent.com/108379254/208484416-838282c6-ea68-4da8-86d2-0bde4eb17042.png)

### Decision Tree
  ![image](https://user-images.githubusercontent.com/108379254/208484595-c9373c90-6920-463f-af8a-42b33aac592d.png)

### K-Nearest Neighbors
  ![image](https://user-images.githubusercontent.com/108379254/208484682-64f01323-9ff8-4d90-a0e8-5258a2ec7968.png)
  
  Since the Deccision Tree has the best recall score, we will use that for modelling and optimization.
  
 ## Tuning Hyperparameters
  #### max_depth
  ![image](https://user-images.githubusercontent.com/108379254/208485011-024eb1b2-08e3-4c56-8e26-d5bf9a6a7e4d.png)

  #### min_samples_split
  ![image](https://user-images.githubusercontent.com/108379254/208485113-4fd41364-d903-48b1-9caa-80accbfceda7.png)

  ####
  ![image](https://user-images.githubusercontent.com/108379254/208485349-a16c2570-3a3d-468c-aaf1-0c259d95ef10.png)

## Building the model with the peak values: 
 ` max_depth:15`
 ` min_samples_split:28`
 ` min_samples_leaf:3`
 
 #### Result with the optimized parameters
 ![image](https://user-images.githubusercontent.com/108379254/208486085-64cd36e7-b9a7-4aff-8a9b-293014542c5c.png)

## Checkgin feature_importance
![image](https://user-images.githubusercontent.com/108379254/208486234-550c18df-82fa-4507-98c0-3ca9e60a3c65.png)

#### Using GridSearch on the model using only top10 features
![image](https://user-images.githubusercontent.com/108379254/208486396-de0a3847-af38-4606-974c-07d51ee19df1.png)

#### Random Forest
![image](https://user-images.githubusercontent.com/108379254/208486542-568411c3-edd5-4ada-b7ea-2b45f74c0656.png)

## Visualizing Scores of the model with optimized parameters, GridSearch and RandomForest
![image](https://user-images.githubusercontent.com/108379254/208486709-92d2fe90-b50c-4655-b581-c4c077cc5a3a.png)

## Checking the confusion matrix of model with top10 features Vs all_features
 ![image](https://user-images.githubusercontent.com/108379254/208487152-068fe9fe-5eeb-4723-b9f6-6b185f37842f.png)

We can see that the features make no difference

## Examining target feature
![image](https://user-images.githubusercontent.com/108379254/208487444-ba86e765-b029-4a20-8935-9892ad24e2b0.png)

We can see clearly that there is an imbalance in the different classes.
We will now train a model on a balanced dataset and test it on the validation data to see check for model performance.

## Confusion Matrix between balanced and unbalanced data
![image](https://user-images.githubusercontent.com/108379254/208487834-de3520b7-a395-4e5e-99b8-8e0b26ea48ab.png)

# Next Steps
1. Possibly re-frame this as a binary classification problem i.e functional vs non-functional and see if we can build a better model. 
2. Re-create the model with equal number of data points between functional and non-functional. Optimize parameters on this balanced dataset and test it on validation data to check for performance.





