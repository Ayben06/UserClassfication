# Machine Learning for User Classification Project
## Business Case

Machine learning’s numerous implications include improving business decision-making. This project provides a practical illustration of this use case. It focuses on predicting the likelihood of a student registered for a free plan purchasing a subscription on the platform. The decision is based on students’ activities on the platform—viewing lectures and participating in exams.

The project is inspired by an initiative in 2022 to predict student purchases before the Black Friday campaign. The project aims to create a list of students likelier to purchase and retarget them with unique ads on social media. But as it turned out, this was no easy task due to the extreme imbalance of the data—the number of students who had never purchased a subscription was much higher than the number of students who had. 

As you will see, such class imbalance combined with humans’ unpredictable behavior makes it challenging to predict student purchases.

## Database
The database I worked with consists of seven columns used as predictor variables and one as a target variable (the `purchased` column). The target variable is a binary column where `0` indicates a student who hasn’t bought a subscription and `1` represents a student who has. Predictor variables store metrics related to student behavior recorded during the free-plan period.

## Data Preprocessing
### Importing the Database
Import and analyze the dataset. The first step to creating a machine learning model is importing the data source. Import the data in the ml_datasource.csv file and carefully study the output.
### Removing Outliers
Examine the distribution plots of the numerical features and study their skewness.Remove data points from the `DataFrame` that meet the following criteria:

   - Minutes watched larger than 1,000
   - Number of courses surpassing 10
   - Number of practice exams started higher than 10
   - Minutes spent on exams going beyond 40 minutes
    
   We could’ve lowered the cutoffs and reduced the skewness of the data even more. Still, we should be careful with removing too many datapoints—as a rule of thumb, we should remove
   no more than 5%. Additionally, we should remember that the data is heavily imbalanced, and removing too many datapoints from the minority class would lead to inaccurate predictions.
   - To study the data distributions without outliers, create all six subplots anew using the `data_no_outliers` `DataFrame`.

### Checking for Multicollinearity
Identify and remove highly correlated feature variables. The term ‘multicollinearity’ refers to a situation where two or more independent variables in a regression model are highly linearly related. Such a problem can make it difficult to determine the individual effect of predictors on the dependent variable and can lead to unstable coefficient estimates.


Although this project considers a classification rather than a regression problem, removing related feature variables is still important. A logistic regression model, for example, assumes its predictors are independent. Moreover, dealing with multicollinearity helps reduce the dimensionality (the number of feature variables) of a problem; high dimensionality is an issue that the k-nearest neighbors model, for instance, could suffer from. (Decision trees and random forests are seldom affected by multicollinearity.)


The Variance Inflation Factor (VIF) is a measure used to detect the presence of multicollinearity in a dataset. A value of 1 indicates that the features are not correlated, while a value greater than 1 suggests the presence of a correlation. As a rule of thumb, a variable with a VIF value higher than 5 indicates problematic multicollinearity.


Your task now is to check for multicollinearity in the data using the variance inflation factor (VIF) metric. Identify and remove the numerical feature with the highest VIF value. This is done because this feature is likely redundant with others in the dataset, and its removal can help reduce multicollinearity. After removing the column, calculate the VIF values again for the remaining numerical features. Now identify the feature with the highest VIF value.

### Dealing with NaN Values
Replace NaN values in the `student_country` column. As it turns out, the string NA in the database refers to the country code of Namibia. But after importing the CSV file into a pandas DataFrame, this country code has been translated to     NaN. Substitute all NaN values in the student_country column with the string `NAM`.
### Splitting the Data
Now that the data’s been preprocessed, it’s time to split it into targets and inputs. The former should include only the purchased column, while the latter should contain all columns except the purchased one.
### Encoding the Data
Before feeding the data to any training algorithm, we must store all features as numerical values. We should therefore deal with the student_country column storing values of a string data type. In this project, we’ll achieve this using the OrdinalEncoder class provided by `sklearn`. 

## Creating Models
### Logistic Regression Model
Create a logistic regression model using the training data and the `Logit()` function from the `statsmodels` library. Output the result’s summary. Then, predict the outcome of the test data.

- If the predicted probability is smaller than or equal to 0.5, consider the prediction 0—the student won’t purchase a subscription.
- If the predicted probability is larger than 0.5, consider the prediction 1—the student will purchase a subscription.

Create a confusion matrix of predictions.

![lgt_confusionmatrix](https://github.com/Ayben06/UserClassfication/assets/71720324/99a14a6a-3293-4a88-a3a3-f9168a52c03d)
- Accuracy: The model accurately predicted outcomes for 94.90% of test instances. While high accuracy is important, additional metrics offer a more thorough evaluation.

- Precision: At 87.96%, the model excelled in correctly classifying positive instances, crucial when minimizing false positives is a priority.

- Recall: With a recall of 51.69%, the model effectively captured a substantial portion of actual positive instances, vital when minimizing false negatives is a priority.

- F1-score: The F1-score, balancing precision and recall, stands at 65.12%, providing a comprehensive measure of overall performance.

### K-Nearest Neighbors Model
Use the training data and `sklearn`’s `GridSearch` optimizer to find the best K-nearest neighbors model. Let the decision for the best model be based on the accuracy score. Consider the following range of parameters:

- Number of neighbors – between 1 and 50, inclusive
- Weights – uniform and distance

Build a confusion matrix and print a classification report.

### Support Vector Machines Model
Use the training data and `sklearn`’s `GridSearch` optimizer and `SVC` (Support Vector Classification) estimator to find the best support vector machines model. Let the decision for the best model again be based on accuracy. Consider the following range of parameters:

- `kernel` – `linear`, `poly`, or `rbf`
- `C` – between 1 and 10, inclusive
- `gamma` – `scale` or `auto`.

Before feeding the training data to the model, I use `sklearn`'s `MinMaxScaler` function to constrict the features in ranges between -1 and 1.

To test the model, build a confusion matrix and print a classification report.

### Decision Trees Model
Use the (non-scaled) training data and `sklearn`’s `GridSearch` and `DecisionTreeClassifier` functions to find the best decision tree model. Let the best model be determined based on accuracy. Loop only through the parameter ccp_alpha and test the values 0, 0.001, 0.002, 0.003, 0.004, and 0.005. 

I use the `plot_tree` function to generate a graphical representation of the decision tree.

![decisiontree](https://github.com/Ayben06/UserClassfication/assets/71720324/81827c0d-847b-4722-9e9b-2416b0ae98ad)


Display the decision tree, build a confusion matrix, and print a classification report. Interpret the results.

### Random Forests Model
Using `sklearn`’s `RandomForestClassifier` and the ccp_alpha value that gave the best accuracy in Decision Trees Model, create a Random Forest model.
Display the confusion matrix and classification report of the model.

## Observations:
   * Logistic Regression: Achieves a good accuracy but has a lower recall for the positive class, indicating that it may not capture all positive instances.

   * K-Nearest Neighbors: Balanced precision and recall, indicating a good overall performance.

   * Support Vector Machines: High precision but lower recall for the positive class, suggesting it may miss some positive instances.

   * Decision Tree: Balanced precision and recall, similar to K-Nearest Neighbors.

   * Random Forest: Similar performance to the Decision Tree, with a slightly higher precision.

## Conclusion:
   * Accuracy alone is not enough to determine the best model. It's important to consider precision and recall, especially if the data is imbalanced.

   * K-Nearest Neighbors and Decision Tree seem to provide a good balance between precision and recall, making them strong candidates.

   * Random Forest performs well, providing a good balance between precision and recall.

   * Logistic Regression and Support Vector Machines may need further tuning or consideration of different evaluation metrics, especially if the goal is to improve recall for the positive class.
