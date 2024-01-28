# Machine Learning for User Classification Project
## Business Case

Machine learning’s numerous implications include improving business decision-making. This project provides a practical illustration of this use case. It focuses on predicting the likelihood of a student registered for a free plan purchasing a subscription on the platform. The decision is based on students’ activities on the platform—viewing lectures and participating in exams.

The project is inspired by an initiative in 2022 to predict student purchases before the Black Friday campaign. The project aims to create a list of students likelier to purchase and retarget them with unique ads on social media. But as it turned out, this was no easy task due to the extreme imbalance of the data—the number of students who had never purchased a subscription was much higher than the number of students who had. 

As you will see, such class imbalance combined with humans’ unpredictable behavior makes it challenging to predict student purchases.

## Database
The database I worked with consists of seven columns used as predictor variables and one as a target variable (the `purchased` column). The target variable is a binary column where `0` indicates a student who hasn’t bought a subscription and `1` represents a student who has. Predictor variables store metrics related to student behavior recorded during the free-plan period.

## Data Preprocessing
1. **Importing the Database**: Import and analyze the dataset.The first step to creating a machine learning model is importing the data source. Import the data in the ml_datasource.csv file and carefully study the output.
2. **Removing Outliers**: Examine the distribution plots of the numerical features and study their skewness.
   Remove data points from the `DataFrame` that meet the following criteria:

   - Minutes watched larger than 1,000
   - Number of courses surpassing 10
   - Number of practice exams started higher than 10
   - Minutes spent on exams going beyond 40 minutes
We could’ve lowered the cutoffs and reduced the skewness of the data even more. Still, we should be careful with removing too many datapoints—as a rule of thumb, we should remove
no more than 5%. Additionally, we should remember that the data is heavily imbalanced, and removing too many datapoints from the minority class would lead to inaccurate predictions.
   1. To study the data distributions without outliers, create all six subplots anew using the `data_no_outliers` `DataFrame`.
3. **Checking for Multicollinearity**: Identify and remove highly correlated feature variables.
4. **Dealing with NaN Values**: Replace NaN values in the `student_country` column.
   As it turns out, the string NA in database refers to the country code of Namibia. But after importing the CSV file into a pandas DataFrame, this country code has been translated to     NaN. Substitute all NaN values in the student_country column with the string `NAM`.
6. **Splitting the Data**: Split data into training and testing sets.
7. **Encoding the Data**: Convert categorical data into numerical data.

## Creating Models
### Logistic Regression Model
- Train a logistic regression model using `statsmodels`.
- Display the summary and confusion matrix.

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
