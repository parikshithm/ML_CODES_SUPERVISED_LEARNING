Dataset: Admission Prediction
This project uses the 'admit.xlsx' dataset to predict admission status based on several features.

Data Overview

The dataset admit.xlsx contains 400 entries across 5 columns:

admit: The target variable, representing admission status (0 for not admitted, 1 for admitted). This was converted to a categorical data type for analysis.
gre: Graduate Record Examinations score.
gpa: Grade Point Average.
rank: Rank of the undergraduate institution.
gender: Gender of the applicant.
Preprocessing Steps

Target Variable Identification:

The admit column was identified as the class label (Y) and converted to a categorical data type.
Predictor Variables Selection:

The gre, gpa, rank, and gender columns were selected as the predictor variables (X_features).
Data Splitting:

The dataset was split into training and testing sets to evaluate model performance.
X_train, X_test, y_train, and y_test were created with a test size of 0.3 (meaning 30% of the data was allocated for testing, and 70% for training) and a random state of 500 to ensure reproducibility of the split.
Categorical Feature Encoding:

The gender column, being a categorical variable, was converted into a numerical format using one-hot encoding via pd.get_dummies().
drop_first=True was applied to prevent multicollinearity, resulting in a single gender_Male column (where 1 typically represents Male and 0 represents Female).
Both X_train and X_test underwent this encoding to become X_train_encoded and X_test_encoded, respectively.
These preprocessing steps prepare the data for building and training a classification model to predict admission outcomes.



Dataset: Attrition Prediction
This project uses the 'attrition.xlsx' dataset to predict employee attrition based on several features.

Data Overview

The dataset attrition.xlsx contains 1470 entries across 11 columns:

Attrition: The target variable, representing attrition status (0 for no attrition, 1 for attrition). This was converted to a categorical data type for analysis.
EmpID: Employee ID (removed from predictor variables).
Department: Department of the employee.
DistanceFromHome: Distance from home to workplace.
Gender: Gender of the employee.
HourlyRate: Hourly rate of the employee.
MonthlyIncome: Monthly income of the employee.
NumCompaniesWorked: Number of companies worked for.
OverTime: Whether the employee works overtime.
PercentSalaryHike: Percentage salary hike.
JobSatisfaction: Job satisfaction level.
Preprocessing Steps

Target Variable Identification:

The Attrition column was identified as the class label (Y) and converted to a categorical data type.
Predictor Variables Selection:

The EmpID and Attrition columns were excluded. The remaining columns (Department, DistanceFromHome, Gender, HourlyRate, MonthlyIncome, NumCompaniesWorked, OverTime, PercentSalaryHike, JobSatisfaction) were selected as the predictor variables (X_features).
Data Splitting:

The dataset was split into training (X_train, y_train) and testing (X_test, y_test) sets to evaluate model performance.
A test size of 0.3 (meaning 30% of the data was allocated for testing, and 70% for training) and a random state of 500 were used to ensure reproducibility of the split.
All subsequent data processing was performed after the split to prevent data leakage.
Categorical Feature Encoding:

The categorical columns (Department, Gender, OverTime) were converted into a numerical format using one-hot encoding via pd.get_dummies().
drop_first=True was applied to prevent multicollinearity.
Both X_train and X_test underwent this encoding to become X_train_encoded and X_test_encoded, respectively.
Continuous Feature Normalization:

The continuous columns (DistanceFromHome, HourlyRate, MonthlyIncome, NumCompaniesWorked, PercentSalaryHike, JobSatisfaction) were normalized using MinMaxScaler.
This scaling transforms features to a common range (typically 0 to 1), which is beneficial for many machine learning algorithms.
The scaler was fit_transform on X_train_encoded and transform on X_test_encoded for consistency.
These preprocessing steps prepare the data for building and training a classification model to predict employee attrition.


Business Decision

Objective: Build a predictive model to identify defaulters, i.e., high-risk individuals.

Code Imports

The first code cell imports necessary libraries:

pandas for data manipulation.
matplotlib.pyplot for plotting.
seaborn for enhanced visualizations.
sklearn (Scikit-learn) for machine learning functionalities.
Load Data

The code loads an Excel file named 'ClassifyRisk.xlsx' into a pandas DataFrame called raw_df.

Display Head of DataFrame

raw_df.head() displays the first 5 rows of the DataFrame, providing a quick look at the data structure and content.

Output of raw_df.head():
mortgage  loans  age marital_status  income  risk
0        y      3   34          other   28061     1
1        n      2   37          other   28009     1
2        n      2   29          other   27615     1
3        y      2   33          other   27287     1
4        y      2   39          other   26954     1

Get DataFrame Information

raw_df.info() provides a concise summary of the DataFrame, including:

The number of entries (rows).
The number of columns.
The non-null count for each column, indicating missing values.
The data type (Dtype) of each column.
Memory usage.
Output of raw_df.info():
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 246 entries, 0 to 245
Data columns (total 6 columns):

Column Non-Null Count Dtype
 0   mortgage        246 non-null    object
1   loans           246 non-null    int64
2   age             246 non-null    int64
3   marital_status  246 non-null    object
4   income          246 non-null    int64
5   risk            246 non-null    int64
dtypes: int64(4), object(2)
memory usage: 11.7+ KB
This output shows that there are 246 entries and no missing values in any of the columns. 'mortgage' and 'marital_status' are object type (categorical), while 'loans', 'age', 'income', and 'risk' are integer types.

Get Descriptive Statistics

raw_df.describe() generates descriptive statistics of the numerical columns in the DataFrame, such as count, mean, standard deviation, min, max, and quartiles.

Output of raw_df.describe():
loans         age        income        risk
count  246.000000  246.000000    246.000000  246.000000
mean     1.308943   40.642276  38789.593496    0.500000
std      0.843995   10.897017  13882.715928    0.501019
min      0.000000   17.000000  15301.000000    0.000000
25%      1.000000   32.000000  26881.250000    0.000000
50%      1.000000   41.000000  37662.500000    0.500000
75%      2.000000   50.000000  49398.500000    1.000000
max      3.000000   66.000000  78399.000000    1.000000

Identify the Class Label or Y variable

The risk column is identified as the target variable (Y) and converted to a 'category' data type, which is often beneficial for classification tasks.

Output of y.info():
<class 'pandas.core.series.Series'>
RangeIndex: 246 entries, 0 to 245
Series name: risk
Non-Null Count  Dtype

246 non-null    category
dtypes: category(1)
memory usage: 502.0 bytes

Select the Predictor Variables into a list called X_features

All columns except 'risk' are selected as predictor variables (X_features).

Output of X_features:
['mortgage', 'loans', 'age', 'marital_status', 'income']

Create X DataFrame

A new DataFrame X is created containing only the predictor variables.

Split data into Training (0.7) and Testing (0.3)

The data is split into training and testing sets using train_test_split from sklearn.model_selection.

X_train, y_train: 70% of the data for training the model.
X_test, y_test: 30% of the data for evaluating the model.
random_state=500 ensures reproducibility of the split.
Output of y_train.info:
<bound method Series.info of 70      1
162     0
163     0
236     0
1       1
..
206     0
17      1
65      1
183     0
90      1
Name: risk, Length: 172, dtype: category
Categories (2, int64): [0, 1]>

Pre-process X-vars

1. Identify and dummy code (one-hot encoding) the categorical column
Categorical columns (mortgage and marital_status) are converted into numerical format using one-hot encoding with pd.get_dummies().

drop_first=True is used to avoid multicollinearity by dropping the first category for each feature.
dtype=int ensures the new dummy variables are of integer type.
Check X_train_encoded Info

X_train_encoded.info() displays the information of the training DataFrame after one-hot encoding.

Output of X_train_encoded.info():
<class 'pandas.core.frame.DataFrame'>
Index: 172 entries, 70 to 90
Data columns (total 6 columns):

Column Non-Null Count Dtype
0   loans                  172 non-null    int64
1   age                    172 non-null    int64
2   income                 172 non-null    int64
3   mortgage_y             172 non-null    int32
4   marital_status_other   172 non-null    int32
5   marital_status_single  172 non-null    int32
dtypes: int32(3), int64(3)
memory usage: 7.4 KB
This shows that 'mortgage' and 'marital_status' have been transformed into numerical dummy variables.

Display Head of X_train_encoded

X_train_encoded.head() displays the first 5 rows of the encoded training DataFrame.

Output of X_train_encoded.head():
loans  age  income  mortgage_y  marital_status_other  marital_status_single
70       2   25   23580           1                     1                      0
162      1   66   42120           0                     0                      0
163      1   56   51684           1                     0                      0
236      0   44   50793           1                     0                      0
1        2   37   28009           0                     1                      0
