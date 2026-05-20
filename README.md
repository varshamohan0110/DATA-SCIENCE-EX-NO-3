## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.

STEP 2:Clean the Data Set using Data Cleaning Process.

STEP 3:Apply Feature Encoding for the feature in the data set.

STEP 4:Apply Feature Transformation for the feature in the data set.

STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv('data.csv')
df
```
<img width="508" height="355" alt="image" src="https://github.com/user-attachments/assets/5ea40d63-7ca7-417b-bd7b-acc2d7581e65" />

```
from sklearn.preprocessing import OrdinalEncoder,LabelEncoder
climate = ['Cold','Warm','Hot','Very Hot']
ele = OrdinalEncoder(categories=[climate])
ele.fit_transform(df[["Ord_1"]])
```
<img width="348" height="183" alt="image" src="https://github.com/user-attachments/assets/a54f7456-aa86-41d8-8ce3-a305a6b60a0c" />

```
df['bo2'] = ele.fit_transform(df[["Ord_1"]])
df
```

<img width="522" height="350" alt="image" src="https://github.com/user-attachments/assets/274e1682-9da9-4272-b072-b30bb16860c9" />

```
le = LabelEncoder()
df2 = df.copy()
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```

<img width="625" height="350" alt="image" src="https://github.com/user-attachments/assets/117204a4-6877-4c1f-9d7e-7ad374efb223" />

```
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```
<img width="732" height="353" alt="image" src="https://github.com/user-attachments/assets/259a82b9-7d2c-4fd7-9db2-060f5bfd76f7" />

```
from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder()
df3 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["City"]]))
df2 = pd.concat([enc,df3],axis = 1)
df2
```

<img width="806" height="364" alt="image" src="https://github.com/user-attachments/assets/13383726-ab61-4687-9397-9c2708aef561" />

```
from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder()
df3 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["City"]]))
df2 = pd.concat([enc,df3],axis = 1)
df2
```

<img width="837" height="374" alt="image" src="https://github.com/user-attachments/assets/eb6fc277-7b6b-4afe-a582-998b484d1e31" />

```
pd.get_dummies(df,columns=['City'])
```

<img width="946" height="359" alt="image" src="https://github.com/user-attachments/assets/244c5979-717f-4d4f-8511-19fd3dd01e85" />

```
from category_encoders import BinaryEncoder
df = pd.read_csv('data.csv')
df
```

<img width="505" height="355" alt="image" src="https://github.com/user-attachments/assets/d4a3ebdf-b89b-449e-9cae-0adba8f7db9e" />

```
be = BinaryEncoder()
nd = be.fit_transform(df['Ord_2'])
df
```
<img width="476" height="350" alt="image" src="https://github.com/user-attachments/assets/7aa15a63-e0f2-4e34-87ba-bc3b9e275409" />

```
from category_encoders import TargetEncoder
te = TargetEncoder()
CC = df.copy()
new = te.fit_transform(CC["City"],y=CC["Target"])
CC = pd.concat([CC,new],axis = 1)
CC
```
<img width="743" height="352" alt="image" src="https://github.com/user-attachments/assets/88a96781-9f17-4dc8-9f39-7681f3ad60c6" />

```
if 'City' in CC.columns:
    CC = CC.drop('City', axis=1)
new = te.fit_transform(X = df["City"],y=df["Target"])
CC = pd.concat([CC.reset_index(drop=True),new.reset_index(drop=True)],axis = 1)
CC
```

<img width="578" height="362" alt="image" src="https://github.com/user-attachments/assets/11ef9521-1b2b-4b34-91b9-d7987ee8f99b" />

```
df = pd.read_csv('Data_to_Transform.csv')
df
```
<img width="994" height="404" alt="image" src="https://github.com/user-attachments/assets/988ee677-115f-4d69-85df-1ba42687b89c" />

```
df.skew()
```

<img width="516" height="103" alt="image" src="https://github.com/user-attachments/assets/58e9357f-4a9c-494e-85ce-e9952166201c" />

```
np.log(df["Highly Positive Skew"])
```

<img width="528" height="221" alt="image" src="https://github.com/user-attachments/assets/e34aa214-d0c3-44b0-ba3c-0dd2937d15e7" />

```
np.reciprocal(df["Moderate Positive Skew"])
```

<img width="592" height="222" alt="image" src="https://github.com/user-attachments/assets/388d92da-392e-4ec3-b43c-e42296e543ee" />

```
np.sqrt(df["Highly Positive Skew"])
```

<img width="695" height="227" alt="image" src="https://github.com/user-attachments/assets/42627792-de61-4df4-8585-63ed554d9f2c" />

```
np.square(df["Highly Positive Skew"])
```

<img width="680" height="226" alt="image" src="https://github.com/user-attachments/assets/aff52585-ad3f-46f0-ba64-f3615152e0fd" />

```
df["Highly Positive Skew_boxcox"], parameters = stats.boxcox(df["Highly Positive Skew"])
df
```

<img width="1067" height="412" alt="image" src="https://github.com/user-attachments/assets/ce290986-b590-42c3-bb6f-3a67a0a833ce" />

```
df["Moderate Negative Skew_yeojohnson"], parameters = stats.yeojohnson(df["Moderate Negative Skew"])
df
```

<img width="559" height="212" alt="image" src="https://github.com/user-attachments/assets/9f7cccbf-2dc8-4b6c-b45d-4fe99019bf34" />

```
from sklearn.preprocessing import QuantileTransformer
qt = QuantileTransformer(output_distribution = 'normal')
df["Moderate Negative Skew_1"] = qt.fit_transform(df[["Moderate Negative Skew"]])
df
```

<img width="1115" height="438" alt="image" src="https://github.com/user-attachments/assets/4cf06003-42d0-4790-a404-f849a7f7dca0" />

```
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df["Moderate Negative Skew"],line = '45')
plt.show()
```

<img width="846" height="443" alt="image" src="https://github.com/user-attachments/assets/c0c74b07-2850-4a70-b901-6ab80387d951" />

```
sm.qqplot(df["Moderate Negative Skew_1"],line = '45')
plt.show()

```
<img width="723" height="432" alt="image" src="https://github.com/user-attachments/assets/41cf7bcd-90ab-4b57-9a82-c6d99e09d555" />

```
df["Highly Negative Skew_1"] = qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line = '45')
plt.show()
```

<img width="835" height="451" alt="image" src="https://github.com/user-attachments/assets/ec6c935c-4de3-42db-80ba-dec54f661649" />

```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew_1"]),line = '45')
plt.show()
```
<img width="812" height="432" alt="image" src="https://github.com/user-attachments/assets/be9f1d05-98b6-4803-a5c9-b4a910106d7a" />

```
sm.qqplot(df["Highly Negative Skew_1"],line = '45')
plt.show()

```

<img width="726" height="435" alt="image" src="https://github.com/user-attachments/assets/6ccb3495-b251-4426-9ffc-f6145ddefd4d" />

```
sm.qqplot(np.abs(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```
<img width="772" height="431" alt="image" src="https://github.com/user-attachments/assets/2d43d433-f7f9-4e25-a1a4-2879347218db" />

```
sm.qqplot(np.log(df["Highly Negative Skew_1"]),line = '45')
plt.show()
```
<img width="1100" height="483" alt="image" src="https://github.com/user-attachments/assets/b298f8a9-330b-467d-9226-cb9a20307ed3" />


```
sm.qqplot(np.sqrt(df["Moderate Negative Skew_1"]),line='45')
plt.show()
```
<img width="1064" height="476" alt="image" src="https://github.com/user-attachments/assets/12a9320b-83e4-48d5-a292-dcc9869c5583" />

```
pd.concat([CC,new],axis = 1)
```
<img width="562" height="355" alt="image" src="https://github.com/user-attachments/assets/77593da5-cfb7-4236-87f0-ff9484ac78ce" />

# RESULT:
 Thus, we have successfully performed Feature Encoding and Transformation process and saved the data to a file.      

       
