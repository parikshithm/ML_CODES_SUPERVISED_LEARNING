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
