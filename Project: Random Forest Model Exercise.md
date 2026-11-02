# Random Forest Machine Learning Model

## Process
### Data Preprocessing
For this project, I created a Google Colab notebook to execute my code. To train my model, I chose a dataset from Kaggle.com about credit card fraud. I wanted to train my model to take the seven parameters from this dataset and make predictions on whether test transactions are fraudulent or legitimate. The dataset that I used is called “Credit Card Fraud.” (See Figure 1) It is also around 76 MB. I didn’t want to handle these many transactions for just a lab exercise. I might if I want to improve my model’s accuracy in the future, but for now, I shortened it to around three thousand transactions. This was to exceed the minimum lab requirement of one thousand records while working with a feasible amount of data. The large original file took longer periods of time to process. To shorten the dataset, I first downloaded the csv file to my local device. I then ensured that the transactions weren’t sorted in any way, because that would alter the results and cause bias. I then opened PowerShell and ran the command, “Get-Content original.csv -TotalCount 3001 | Out-File new_file.csv -Encoding utf8,” in the appropriate folder to create a new file that only contains the first three thousand transactions in the csv file. The data was ready to be loaded. I then loaded the data into my Colab notebook for processing. I used panda to state the simple characteristics of the dataset. (See Figure 2) After reviewing the data, I found that it was relatively clean. There were outliers, but in the context of detecting anomalous, fraudulent cases, I kept them. I did make sure there weren’t any weird outliers that didn’t make sense, like negative numbers. The final step for data preprocessing was separating it into training data and testing data. (See Figure 3) My “x” variable represents every column except for the “fraud” column. My “y” variable represents the “fraud” column. From these variables, I split the data into training/testing data with an 80/20 ratio, respectively. The data was ready to be processed. 

### Model Choice and Preparation
For my one main method, I chose to use random forest modeling. The reason for this is because it is a classification problem with binary data. I couldn’t use regression analysis for my target variable (fraud). From the classification options, random forest modeling was the best choice, because it can capture the non-linear trends of fraudulent cases. Each column is a factor, but not the sole determinant. Random forests can simulate many scenarios with minor changes having larger results, making it an ideal tool for handling many variables. It was also an easy modelling process, because there was little preprocessing. With other methods, I would likely have to scale numerical values and standardize each variable. With random forests, the data was already in a compatible format. The data was clean. There were no duplicate records or negative values. I ran some commands to check this. The only preprocessing I needed to perform was splitting the data into input values and target values and then split these variables into training data and testing data. 

### Model Training and Evaluation
I trained the data with one hundred decision trees. I used “random_state=42” to create a reproducible result. I imported RandomForestClassifier from sklearn.ensemble. (See Figure 4) This tool handled the brunt of training the model. After processing the model with training data, I proceeded to the testing phase. Using the built-in tools that I imported, I generated predictions and probabilities for evaluation. There was still not much to see yet, so I used the recall method to display testing results. The recall method was a suitable choice, because the target data was in a countable format, making the calculation simple. It operated by counting successful predictions and making it a percentage of the total prediction. There is a preconfigured recall_score tool, which was very helpful. I ran the tool and printed the results to standard output. (See Figure 5) My initial run achieved an accuracy of 94.44%. I needed to check if this was a fluke and was either a relatively accurate score or a relatively inaccurate score. To do this, I used cross-validation with 5 folds. This required the StratifiedKFold and cross_val_score tools, which I imported. These tools generated recall scores based on shuffled versions of the data. (See Figure 6) The scores ranged from 95.3% to 97.7% accuracy. I was happy to see that my initial run was not uncommonly accurate, but in the general vicinity of the other tests. The average recall score was about 96.8%, and the standard deviation of the results was 1.13%, meaning that the initial run was an uncommonly low recall score for this dataset. I played around with the fold count. When I ran it with four folds, one of the folds achieved 100% accuracy during the testing phase. The relative accuracy between folds tells me that the predictions are relatively stable for this dataset. If I increased the sample size. I would expect an even higher recall rate. After training and evaluating my random forest model. I was ready for visualization.

## Results
### Findings
One of my favorite parts of this exercise was seeing the importance factor for each column. (See Figure 7) The most important factor in determining the validity of a card transaction is ratio to median purchase price. I would not have originally guessed this, but the data shows that, to predict fraudulent transactions, over half of the weight goes to this factor. Looking back, this makes sense, because this column can detect anomalies from normal behavior. The next most important factor was distance from home. Then whether it was an online order or not. The rounded weight given to each category was 54% to ratio to median purchase price, 21% to distance from home, 12% to online status, 8% to distance from last transaction, 3% to pin number usage, 2% to chip usage, and less than 1% to repeat retailer status. Another method to visualize my results was using a confusion matrix. (See Figure 8) It works by graphing actual data numbers with predicted numbers. For example, I was able to clearly see that there were three incorrect predictions with this visual. I could also see that all three were false negatives. There were no false positives. It correctly predicted the other sample transactions. It was also very user-friendly with colors and easy-to-understand format. 

### Retrospect
If I were to continue developing this model, I'd set up several methods of evaluation, such as R2, accuracy, or precision. While using recall-score and confusion matrix for initial evaluation methods was a good start for this lab exercise, I'd implement several evaluation methods to better measure the success of my model. I'd also experiment with other models, such as gradient boosting classifier, support vector machine (SVM), or neural networks. These can process data to find non-linear trends. The credit card fraud dataset I've been using has multiple types of data, and may have several complex indicators of fraud. I would also increase the size of my dataset. I originally reduced the size of the dataset to improve performance in my Colab environment, but in real-life scenarios, I'd use many more records to improve accuracy.  

## Conclusion
The main takeaways from this exercise are that the model runs with reasonable accuracy, and that the most important factor when determining fraudulent transactions is the ratio to median transaction. There is a direct correlation between the ratio and the likelihood of credit card fraud. The feature importances and the confusion matrix back these conclusions. For future reference, I’d train the model with larger amounts of data for a more consistent prediction. The dataset I used has many more recorded transactions to analyze data from. Personally, I loved this challenge, because it gave me a basis for training simple models for machine learning. This model could be exported into different formats to create an open form that predicts fraudulent credit card transactions within a specified confidence interval. I can see the direct benefit of developing this into a more refined tool in the future. I also enjoyed the critical thinking that this type of project requires.

## Appendices
<details>
  <summary> Click to view Figures </summary>

  - Link to dataset: https://www.kaggle.com/datasets/dhanushnarayananr/credit-card-fraud
 
- Figure 1: Chosen dataset
<img width="979" height="189" alt="image" src="https://github.com/user-attachments/assets/6aaac890-d79e-4852-8961-a5cf0f3f742f" />

- Figure 2: Load into panda
<img width="796" height="509" alt="image" src="https://github.com/user-attachments/assets/cefc3414-14f0-4b84-b0d0-ee7eefd081f3" />

- Figure 3: Data separation into training and testing data
<img width="723" height="238" alt="image" src="https://github.com/user-attachments/assets/2e7be35f-2a61-4ad2-9def-d2bcccd49ab2" />

- Figure 4: Training process
<img width="848" height="385" alt="image" src="https://github.com/user-attachments/assets/dfca2cda-ae4e-4ba3-bb2e-a170f55f7643" />

- Figure 5: Recall score evaluation
<img width="593" height="237" alt="image" src="https://github.com/user-attachments/assets/aa926d1e-6f2d-4fa3-a199-b073b7863c95" />

- Figure 6: Cross-evaluation scores
<img width="641" height="550" alt="image" src="https://github.com/user-attachments/assets/d8f917f4-57f2-4fd7-b6c4-056fc348fb19" />

- Figure 7: Importance weights for each feature
<img width="979" height="508" alt="image" src="https://github.com/user-attachments/assets/d0c3af4b-e6ca-4e94-9ad7-c528e4c2b782" />

- Figure 8: Confusion matrix visual tool
<img width="712" height="538" alt="image" src="https://github.com/user-attachments/assets/5b50f11d-43a7-4a7e-b3d4-2c0686000e99" />

  
</details>
