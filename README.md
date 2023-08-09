# Water Pump Classifier

## Description
  To help the Goverment of Tanzania monitor the condition of installed waterpumps across the country.Given a set of parameters, the model should be able to     predict the status of a waterpump. Status can be as classified as:

1. Functional
2. Functional needs repair
3. Non functional
  
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
  
  Since the Decision Tree has the best recall score, we will use that for modelling and optimization.
  
 ## Tuning Hyperparameters
  #### max_depth
  ![image](https://user-images.githubusercontent.com/108379254/208558657-1db67aa9-92b6-4938-a5a0-d14a32ab7c88.png)

  #### min_samples_split
  ![image](https://user-images.githubusercontent.com/108379254/208558728-9246d916-5087-4348-9958-7804f0637386.png)

  #### min_samples_leaf
  ![image](https://user-images.githubusercontent.com/108379254/208558776-4d86a064-9b9b-44c3-aeaf-526efc745092.png)


## Building the model with the peak values: 
 ` max_depth:20`
 ` min_samples_split:21`
 ` min_samples_leaf:3`
 
 #### Result with the optimized parameters
 ![image](https://user-images.githubusercontent.com/108379254/208558949-49c71cdd-2bf4-48b1-afc3-8f5af0a47a40.png)

## Checking feature_importance
![image](https://user-images.githubusercontent.com/108379254/208559008-5b8b0795-9771-46a0-9c7a-585a2ae68c18.png)

#### Using GridSearch on the model using only top10 features
![image](https://user-images.githubusercontent.com/108379254/208559091-9fed5cc8-6b97-42e6-9a25-c00302b92e39.png)

#### Random Forest
![image](https://user-images.githubusercontent.com/108379254/208559136-8694b7f7-007e-48c1-922b-c8d2a4941b03.png)


## Visualizing Scores of the model with optimized parameters, GridSearch and RandomForest
![image](https://user-images.githubusercontent.com/108379254/208559170-a368a12e-ce10-41e5-9a88-a82e1cdea3ae.png)


## Checking the confusion matrix of model with top10 features Vs all_features
![image](https://user-images.githubusercontent.com/108379254/208559334-bee72be7-f4b6-4655-a4f3-4ac1842dde2e.png)


We can see that the features make a negligible difference.

## Examining target feature
![image](https://user-images.githubusercontent.com/108379254/208487444-ba86e765-b029-4a20-8935-9892ad24e2b0.png)

We can see clearly that there is an imbalance in the different classes.
We will now train a model on a balanced dataset and test it on the validation data to see check for model performance.

## Confusion Matrix between balanced and unbalanced data
![image](https://user-images.githubusercontent.com/108379254/208559440-0e82e9e8-0fb7-4b1b-9a4f-96afb4f7b6b1.png)

# Next Steps
1. Possibly re-frame this as a binary classification problem i.e functional vs non-functional and see if we can build a better model. 
2. Re-create the model with equal number of data points between functional and non-functional. Optimize parameters on this balanced dataset and test it on validation data to check for performance.

# More Information
 - [Notebook](phase3_project.ipynb)
 - [Presentation](presentation.pdf)

## Repository Structure

```
├── README.md
├── notebook.pdf
├── phase3_project.ipynb
├── presentation.pdf
└── repo.pdf
```


