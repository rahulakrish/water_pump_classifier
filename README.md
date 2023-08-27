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

## Non-functional Pump deep-dive
 Before modelling, it is worth looking at the data to see if we can uncover any patterns from the data:

#### Non-functional pumps by Age
The older the pump, the more likely it is to fail. We can run a histogram plot to check the rate of failures by age of the pumps:

![age](https://github.com/rahulakrish/water_pump_classifier/assets/108379254/f55bd8c2-4b89-437d-b237-5eeda3b26bf2)

From the plot, it is quite clear that there is a gap in data collection with majority of the pumps having no information about when they were installed. It is also surprising to see that the newer pumps have a higher failure rate compared to the older pumps.

#### Non-fuctional pumps by Installer
From the data, there are 1201 companies that have installed the pumps.Are there certain installers who have more mal fucntioning pumps than others? Visualizing all 1201 companies is difficult given the size, but we can look at the top 20 companies with the most failures:

 ![installer](https://github.com/rahulakrish/water_pump_classifier/assets/108379254/ab1bb622-85e5-4740-955e-d339447ac11c)

It is quite clear to see that pumps installed by DWE far outnumber the rest of the companies by factor of almost 7.
Another question that can be asked is why one single company was given the responsibility with installing so many pumps.

#### Non functional pumps by Management
Like the installers, we can also check to see if certain companies tasked with managing the pumps perform worse compared to the others:

![mgmt](https://github.com/rahulakrish/water_pump_classifier/assets/108379254/95f278b4-f885-4ac5-9247-05565e7470ce)


#### Non-functional pumps by Subvillage
We can plot non-functional pumps by region to see so we can focus our attention on the areas most affected right away:

![vill](https://github.com/rahulakrish/water_pump_classifier/assets/108379254/a4bc7622-7027-4672-8275-e829004cd64c)


 ## Test Scores of baseline models
| Model         | f1_score |
|---------------|----------|
| Log_reg       | 0.709    |
| Decision_tree | 0.747    |
| KNeighbors    | 0.763    |
  
 Since the Decision Tree has is much faster and provides more avenues for tuning, let's move forward with it.
  
 ## Tuning Hyperparameters
  #### max_depth
  
![d](https://github.com/rahulakrish/water_pump_classifier/assets/108379254/6843fec7-d2e7-4da7-8f0e-5cf133530fb6)


  #### min_samples_split
  
![s](https://github.com/rahulakrish/water_pump_classifier/assets/108379254/1f25b9e0-f411-423b-8665-1738fa72a15e)


  #### min_samples_leaf
  
![l](https://github.com/rahulakrish/water_pump_classifier/assets/108379254/e045ba57-443d-46fe-81de-db55963ae3ef)


## Building the model with the peak values: 
 ` max_depth:19`
 ` min_samples_split:14`
 ` min_samples_leaf:6`

 | Model         | f1_score |
|---------------|----------|
| log_reg       | 0.709    |
| decision_tree | 0.747    |
| k_neighbors    | 0.763    |
| tuned_decision_tree   | 0.757    |
 
## Ensemble Methods
Ensemble methods combine the results of several base estimators. The result would then be the average of all the estimators.

#### Random Forest
One ensemble method called Random Forest works by building N decision trees independently on different sub-samples of data with replacement. The final result will the be the aggregated result from all the individual decision trees.
We'll use the same optimal hyperparameters for the decision trees:

| Model               | f1_score |
|---------------------|----------|
| log_reg             | 0.709    |
| decision_tree       | 0.747    |
| k_neighbors         | 0.763    |
| tuned_decision_tree | 0.757    |
| random_forest       | 0.767    |

We can see that performance gain is marginal.

#### Adaboosting
Adaptive Boosting works by building "weak learners" and iteratively improving model performance. By assigning higher weights to results that the model got wrong and reducing weight for the correct results, successive models are built to focus on the incorrect results and thereby at the end,we have a strong learner that get most of the results correct.

|     **_Model_**     | **_f1_score_** |   
|:-------------------:|:--------------:|
| log_reg             | 0.709          |   
| decision_tree       | 0.747          |   
| k_neighbors         | 0.763          |   
| tuned_decision_tree | 0.757          |   
| random_forest       | 0.767          |  
| ada_boost           | 0.790          |  


#### XGBoost
XGboost, also referred to as 'Extreme Gradient Boosting', is another boosting algorithm like Adaboost. Like Adaboost, XGBoost also builds weak learners and checks for performance. However rather than assign weights to the results, XGBoost calculates the residuals for each data point and then combines the results into a Loss Function to calculate overall loss. Then by using gradient descent, the losses are minimized.

|        Model        | f1_score |
|:-------------------:|:--------:|
|       log_reg       |   0.709  |  
|    decision_tree    |   0.747  |  
|     k_neighbors     |   0.763  |  
| tuned_decision_tree |   0.757  |  
|    random_forest    |   0.767  |  
|      ada_boost      |   0.790  |  
|         xgb         | 0.789    |  

## Class imbalance

We can try to address the class imbalance and convert the problem from a ternary classification to a binary classification problem and see if we get better results.

|        Model        | f1_score 
|:-------------------:|:--------
|       log_reg       |   0.709  
|    decision_tree    |   0.747  
|     k_neighbors     |   0.763  
| tuned_decision_tree |   0.757  
|    random_forest    |   0.767  
|      ada_boost      |   0.790  
|         xgb         |   0.789  
|   xgb_reclassified  |   0.804  

### Confusion matrix

The Confusion Matrix is a graphical representation of `[TP,FP,TN,FN]` values. Let's look at the confusion matrix of the xgb model:

![c](https://github.com/rahulakrish/water_pump_classifier/assets/108379254/67399e54-4b5d-454f-a49a-50e87114345d)


## Limitations

Hyperparameters of the different models can be tuned to extract more performance although this will be very time consuming.

## Next Steps

1. From the [Non-functional pumps deep-dive](#Non-functional-pumps-deep-dive), it is clear to see which regions are suffering the most. Personnel can be deployed straight away to those areas to fix the pumps. More nuanced analysis will uncover more patterns when analyzing the failed pumps.
2. There is also a need to improve the data collection process. There is a lot superfluous data and lot of missing data that needs to be addressed. More nuanced and quality data will definitely aid in building more accurate models.
3. Give that one contractor for both installation and maintenance far outweighs the others in terms of numbers, this could point systemic issues in the ways contracts are awarded or in the worst case point to corruption. Either way, this needs to be addressed for the sake of the citizens of Tanzania.

# Notebook
 - [Notebook](notebook.ipynb)

## Repository Structure

```
├── .gitignore
├── README.md
├── notebook.ipynb
├── tanzania.PNG
└── waterwell.csv
```


