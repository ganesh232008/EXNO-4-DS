# EXNO:4-DS
# AIM:
To read the given data and perform Feature Scaling and Feature Selection process and save the
data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Scaling for the feature in the data set.
STEP 4:Apply Feature Selection for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE SCALING:
1. Standard Scaler: It is also called Z-score normalization. It calculates the z-score of each value and replaces the value with the calculated Z-score. The features are then rescaled with x̄ =0 and σ=1
2. MinMaxScaler: It is also referred to as Normalization. The features are scaled between 0 and 1. Here, the mean value remains same as in Standardization, that is,0.
3. Maximum absolute scaling: Maximum absolute scaling scales the data to its maximum value; that is,it divides every observation by the maximum value of the variable.The result of the preceding transformation is a distribution in which the values vary approximately within the range of -1 to 1.
4. RobustScaler: RobustScaler transforms the feature vector by subtracting the median and then dividing by the interquartile range (75% value — 25% value).

# FEATURE SELECTION:
Feature selection is to find the best set of features that allows one to build useful models. Selecting the best features helps the model to perform well.
The feature selection techniques used are:
1.Filter Method
2.Wrapper Method
3.Embedded Method

# CODING AND OUTPUT:
# READ THE BMI DATASET
```
import pandas as pd 
from scipy import stats 
import numpy as np 
df=pd.read_csv("bmi.csv") 
df
```
<img width="577" height="574" alt="image" src="https://github.com/user-attachments/assets/d650d07a-60c4-47d0-b182-7680092717fb" />

# MAXIMUM ABSOLUTE VALUE CALCULATION
```
max_vals = np.max(np.abs(df[['Height', 'Weight']]), axis=0) 
max_vals
```
<img width="870" height="142" alt="image" src="https://github.com/user-attachments/assets/1a9bbf4d-0edf-4fc6-8fd1-2e775ff53bf8" />

# STANDARD SCALER
```
from sklearn.preprocessing import StandardScaler 
df=pd.read_csv("bmi.csv")
df.head()
```
<img width="868" height="286" alt="image" src="https://github.com/user-attachments/assets/4a96b0c9-1592-4cfe-959a-7658c04bf638" />

```
from sklearn.preprocessing import StandardScaler
import pandas as pd
df=pd.read_csv("bmi.csv")
sc=StandardScaler()
df[['Height','Weight']]=sc.fit_transform(df[['Height','Weight']]) 
df
```
<img width="880" height="569" alt="image" src="https://github.com/user-attachments/assets/8a25eab7-3eb7-4c95-9e57-043108e8d20d" />

# MIN-MAX SCALER
```
from sklearn.preprocessing import MinMaxScaler 
scaler=MinMaxScaler() 
df[['Height','Weight']]=scaler.fit_transform(df[['Height','Weight']]) 
df.head(10)
```
<img width="876" height="457" alt="image" src="https://github.com/user-attachments/assets/f67cd2a4-1bb1-49a9-9dff-94e4509c1de2" />

# MAXIMUM ABSOLUTE SCALER
```
from sklearn.preprocessing import MaxAbsScaler 
scaler = MaxAbsScaler() 
df=pd.read_csv("bmi.csv") 
df.head()
```
<img width="872" height="323" alt="image" src="https://github.com/user-attachments/assets/d5509dbc-47a4-4296-aa7c-ca57d26751b0" />

```
df[['Height','Weight']]=scaler.fit_transform(df[['Height','Weight']]) 
df
```
<img width="872" height="486" alt="image" src="https://github.com/user-attachments/assets/d0309d80-af84-4366-b0b9-1de7421f0eb7" />

# ROBUST SCALER
```
from sklearn.preprocessing import RobustScaler 
scaler = RobustScaler() 
df[['Height','Weight']]=scaler.fit_transform(df3[['Height','Weight']]) 
df.head()
```
<img width="880" height="310" alt="image" src="https://github.com/user-attachments/assets/107237b9-06e6-49a6-ab57-811142b5d9bb" />

```
df=pd.read_csv("income(1) (1).csv")
df.info()
```
<img width="875" height="489" alt="image" src="https://github.com/user-attachments/assets/e969d371-391a-4db3-bba5-cfcd0327a8ff" />

```
categorical_columns = ['JobType', 'EdType', 'maritalstatus', 'occupation', 'relationship', 'race', 'gender', 'nativecountry']
df[categorical_columns] = df[categorical_columns].astype('category')
df[categorical_columns]
```
<img width="875" height="688" alt="image" src="https://github.com/user-attachments/assets/b8999dac-8805-46d3-80e4-a2b842635824" />

```
df[categorical_columns] = df[categorical_columns].astype('category') 
df[categorical_columns] = df[categorical_columns].apply(lambda x: x.cat.codes)
df[categorical_columns]
```
<img width="875" height="508" alt="image" src="https://github.com/user-attachments/assets/64602fa4-0d73-4106-93c1-3925a184b0ae" />

```
X = df.drop(columns=['SalStat'])
y = df['SalStat'] 
k_chi2 = 6 
selector_chi2 = SelectKBest(score_func=chi2, k=k_chi2) 
X_chi2 = selector_chi2.fit_transform(X, y) 
selected_features_chi2 = X.columns[selector_chi2.get_support()] 
print("Selected features using chi-square test:")
print(selected_features_chi2)
```
<img width="737" height="240" alt="image" src="https://github.com/user-attachments/assets/5e6b1337-bbbf-4b46-9f15-87f3aaf0ac04" />


```
import pandas as pd 
from sklearn.feature_selection import SelectKBest, chi2, f_classif
from sklearn.model_selection import train_test_split 
from sklearn.ensemble import RandomForestClassifier 
selected_features = ['age', 'maritalstatus', 'relationship', 'capitalgain', 'capitalloss', 'hoursperweek'] 
X = df[selected_features]
y = df['SalStat']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42) 
rf = RandomForestClassifier(n_estimators=100, random_state=42) 
rf.fit(X_train, y_train)
```
<img width="741" height="299" alt="image" src="https://github.com/user-attachments/assets/0ddba874-9e96-4649-b152-79d7caacfd88" />

```
y_pred = rf.predict(X_test) 
from sklearn.metrics import accuracy_score 
accuracy = accuracy_score(y_test, y_pred)
print(f"Model accuracy using selected features: {accuracy}")
```

<img width="731" height="128" alt="image" src="https://github.com/user-attachments/assets/2f02db34-4a5a-4829-8e7b-9e95db4f2d02" />

```
import numpy as np 
import pandas as pd
from skfeature.function.similarity_based import fisher_score 
from sklearn.ensemble import RandomForestClassifier 
from sklearn.model_selection import train_test_split 
from sklearn.metrics import accuracy_score
categorical_columns = [ 'JobType', 'EdType', 'maritalstatus', 'occupation', 'relationship', 'race', 'gender', 'nativecountry' ]
df[categorical_columns] = df[categorical_columns].astype('category')
df[categorical_columns] = df[categorical_columns].apply(lambda x: x.cat.codes)
df[categorical_columns]
```
<img width="734" height="565" alt="image" src="https://github.com/user-attachments/assets/ffb78a31-9150-47a0-964a-582d55039eb3" />

```
X = df.drop(columns=['SalStat']) 
y = df['SalStat']
k_anova = 5 
selector_anova = SelectKBest(score_func=f_classif,k=k_anova) 
X_anova = selector_anova.fit_transform(X, y)
selected_features_anova = X.columns[selector_anova.get_support()]
print("\nSelected features using ANOVA:") 
print(selected_features_anova)
```
<img width="737" height="234" alt="image" src="https://github.com/user-attachments/assets/4369e7f3-46c9-4cf9-9918-9276b0e159da" />

```
import pandas as pd 
from sklearn.feature_selection import RFE
from sklearn.linear_model import LogisticRegression
df=pd.read_csv("income(1) (1).csv") 
categorical_columns = [ 'JobType', 'EdType', 'maritalstatus', 'occupation', 'relationship', 'race', 'gender', 'nativecountry' ] 
df[categorical_columns] = df[categorical_columns].astype('category')
df[categorical_columns] = df[categorical_columns].apply(lambda x: x.cat.codes) 
df[categorical_columns]
```
<img width="738" height="538" alt="image" src="https://github.com/user-attachments/assets/49ff47e0-c7b6-4a57-b0f9-796e31cfc056" />

```
X = df.drop(columns=['SalStat'])
y = df['SalStat']
logreg = LogisticRegression()
n_features_to_select =6
rfe = RFE(estimator=logreg, n_features_to_select=n_features_to_select) 
rfe.fit(X, y)
```
<img width="1114" height="777" alt="image" src="https://github.com/user-attachments/assets/55a8d219-6660-465a-be17-0e7b0fe09a6e" />
<img width="1106" height="638" alt="image" src="https://github.com/user-attachments/assets/0a12b3d8-e743-4062-ac95-c754e3b94b67" />

# RESULT:
Thus, Feature selection and Feature scaling has been used on the given dataset.
