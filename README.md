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
3. **Checking for Multicollinearity**: Identify and remove highly correlated feature variables. The term ‘multicollinearity’ refers to a situation where two or more independent variables in a regression model are highly linearly related. Such a problem can make it difficult to determine the individual effect of predictors on the dependent variable and can lead to unstable coefficient estimates.

   Although this project considers a classification rather than a regression problem, removing related feature variables is still important. A logistic regression model, for example, assumes its predictors are independent. Moreover, dealing with multicollinearity helps reduce the dimensionality (the number of feature variables) of a problem; high dimensionality is an issue that the k-nearest neighbors model, for instance, could suffer from. (Decision trees and random forests are seldom affected by multicollinearity.)

   The Variance Inflation Factor (VIF) is a measure used to detect the presence of multicollinearity in a dataset. A value of 1 indicates that the features are not correlated, while a value greater than 1 suggests the presence of a correlation. As a rule of thumb, a variable with a VIF value higher than 5 indicates problematic multicollinearity.

   Your task now is to check for multicollinearity in the data using the variance inflation factor (VIF) metric. Identify and remove the numerical feature with the highest VIF value. This is done because this feature is likely redundant with others in the dataset, and its removal can help reduce multicollinearity. After removing the column, calculate the VIF values again for the remaining numerical features. Now identify the feature with the highest VIF value.

4. **Dealing with NaN Values**: Replace NaN values in the `student_country` column.
   As it turns out, the string NA in the database refers to the country code of Namibia. But after importing the CSV file into a pandas DataFrame, this country code has been translated to     NaN. Substitute all NaN values in the student_country column with the string `NAM`.
6. **Splitting the Data**: Now that the data’s been preprocessed, it’s time to split it into targets and inputs. The former should include only the purchased column, while the latter should contain all columns except the purchased one.
7. **Encoding the Data**: Before feeding the data to any training algorithm, we must store all features as numerical values. We should therefore deal with the student_country column storing values of a string data type. In this project, we’ll achieve this using the OrdinalEncoder class provided by sklearn. 

## Creating Models
### Logistic Regression Model
Create a logistic regression model using the training data and the `Logit()` function from the `statsmodels` library. Output the result’s summary. Then, predict the outcome of the test data.

- If the predicted probability is smaller than or equal to 0.5, consider the prediction 0—the student won’t purchase a subscription.
- If the predicted probability is larger than 0.5, consider the prediction 1—the student will purchase a subscription.

Create a confusion matrix of predictions.
- Accuracy: The model accurately predicted outcomes for 94.90% of test instances. While high accuracy is important, additional metrics offer a more thorough evaluation.

- Precision: At 87.96%, the model excelled in correctly classifying positive instances, crucial when minimizing false positives is a priority.

- Recall: With a recall of 51.69%, the model effectively captured a substantial portion of actual positive instances, vital when minimizing false negatives is a priority.

- F1-score: The F1-score, balancing precision and recall, stands at 65.12%, providing a comprehensive measure of overall performance.

### K-Nearest Neighbors Model
- Use GridSearch to find the best KNN model.
- Display the confusion matrix and classification report.

### Support Vector Machines Model
- Scale features using MinMaxScaler.
- Use GridSearch to find the best SVM model.
- Display the confusion matrix and classification report.

### Decision Trees Model
- Use GridSearch to find the best decision tree model.
- Display the decision tree, confusion matrix, and classification report.

### Random Forests Model
- Train a random forests model using the best `ccp_alpha`.
- Display the confusion matrix and classification report.

## Results Interpretation
1. **Logistic Regression Model**
    - LLR p-value: [Provide the actual p-value and interpretation]
    - Logit model equation: [Provide the equation]

2. **Decision Trees Model**
    - Influential features: [List the features]

3. **Confusion Matrices and Classification Reports**
    - Analyze and interpret the results.

## Conclusion
Summarize key findings, limitations, and potential improvements.
