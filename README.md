## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
```
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.
```
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
df=pd.read_csv("Encoding Data.csv")
df
```
![1](https://github.com/user-attachments/assets/c533d096-41a5-4060-995c-b8a19f422835)

```
df.tail()
```
![2](https://github.com/user-attachments/assets/343029c7-da56-4cdf-b6f8-186bbba33405)

```
df.describe()
```
![3](https://github.com/user-attachments/assets/2e7086c5-3f24-49ca-9121-2b6414d29f6f)


```
df.info()
```
![4](https://github.com/user-attachments/assets/60bb1841-902f-4f38-aced-ccaea8338449)

```
df
```
![5](https://github.com/user-attachments/assets/ebb14d2f-91db-4456-9315-6552d23aa28a)
```
#ordinal encoder
from sklearn.preprocessing import LabelEncoder, OrdinalEncoder
pm=['Hot', 'Warm','Cold']
oe=OrdinalEncoder(categories=[pm])
oe.fit_transform(df[["ord_2"]])
```
![6](https://github.com/user-attachments/assets/e0c2846c-daa8-48a5-9ca0-24f5c7ca475b)
```
df['bo2']=oe.fit_transform(df[["ord_2"]])
df
```
![7](https://github.com/user-attachments/assets/4fb90362-5d4a-4afc-b388-1722bb12061d)
```
#label Encoder
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc
```
![8](https://github.com/user-attachments/assets/a4286fed-0181-4296-940d-80a176118a58)
```
#One hot encoder
from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder(sparse = False)
df2=df.copy()
enc=pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))
df2=pd.concat([df2,enc],axis=1)
df2
```
![9](https://github.com/user-attachments/assets/d6b26101-4de6-41f4-8ad3-a34e622e2ea2)
```
pd.get_dummies(df2,columns=["nom_0"])
```
![10](https://github.com/user-attachments/assets/05e6a774-f43b-4a14-85a7-d8355e122535)
```
pip install --upgrade category_encoders
from category_encoders import BinaryEncoder
df= pd.read_csv("data.csv")
df
```
![11](https://github.com/user-attachments/assets/adad99ef-4103-4f45-916c-416693f2cd8b)
```
#binary encoder
be = BinaryEncoder()
nd=be.fit_transform(df['Ord_2'])
dfb=pd.concat([df,nd],axis=1)
dfb1=df.copy()
dfb

```
![12](https://github.com/user-attachments/assets/a8b28976-336a-4a94-b0b7-2051b3bdd817)
```
#target encoder
from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
new = te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc
```
![13](https://github.com/user-attachments/assets/de1a6c2a-b47c-4adf-b09f-92a32e81a2f4)
```
#Feature Transformation
import pandas as pd
from scipy import stats
import numpy as np
df=pd.read_csv("Data_to_Transform.csv")
df
```
![14](https://github.com/user-attachments/assets/0894de20-a36e-4e32-9727-3159ae7f33b5)
```
df.info()
```
![15](https://github.com/user-attachments/assets/138b2b64-6de5-49d5-9e69-f00b4970be90)
```
df.describe()
```
![16](https://github.com/user-attachments/assets/6ec86a6a-f9ce-4132-9918-7cdb6e54a28d)
```
df.size
```
![17](https://github.com/user-attachments/assets/b515f066-cd64-4246-bbf2-58a449aa0d10)
```
df.skew()
```
![18](https://github.com/user-attachments/assets/c676fe19-3c96-498c-992c-8c0ad633fa17)
```
np.log(df["Highly Positive Skew"])
```

![19](https://github.com/user-attachments/assets/cb824ebc-8898-46c7-a784-7c769b0351b2)

```
np.reciprocal(df["Moderate Positive Skew"])
```

![20](https://github.com/user-attachments/assets/11bd3e30-9271-41f1-b4a9-a77593ef263c)
```
np.sqrt(df["Highly Positive Skew"])
```

![21](https://github.com/user-attachments/assets/4a44fe07-fdda-4f5a-8a36-bc29f81e0021)
```
np.square(df["Highly Positive Skew"])
```

![19](https://github.com/user-attachments/assets/811e4346-41fd-4748-b650-63a2920856ad)
```
df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
df
```
![Screenshot 2024-10-08 131257](https://github.com/user-attachments/assets/76610c52-ee03-4d23-b7c1-2f0ee0668cd6)
```
df["Moderate Negative Skew_yeojohnson"],parameters =stats.yeojohnson(df["Moderate Negative Skew"])
df
```
![Screenshot 2024-10-08 131307](https://github.com/user-attachments/assets/c3f45f0c-2af9-46e3-ac34-9affe30e14d6)
```
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df['Moderate Negative Skew'],line='45')
plt.show()
```
![Screenshot 2024-10-08 131322](https://github.com/user-attachments/assets/32d035cf-3050-4626-93ad-594fad18abe9)
```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```

![Screenshot 2024-10-08 131329](https://github.com/user-attachments/assets/e6624fb2-048e-41ca-806d-bab62371d6be)
```
df
```

![Screenshot 2024-10-08 131337](https://github.com/user-attachments/assets/ae7c5025-9faf-46cf-8d12-fba3e04c3451)
```
df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df['Moderate Negative Skew'],line='45')
plt.show()
```

![Screenshot 2024-10-08 131345](https://github.com/user-attachments/assets/9690e77b-b82a-4b67-9f98-86702846ddcf)

```
df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df['Highly Negative Skew'],line='45')
plt.show()
```

![Screenshot 2024-10-08 131352](https://github.com/user-attachments/assets/03003f9a-861c-43a8-854f-7d2f03b2cefd)
```
sm.qqplot(df["Highly Negative Skew_1"],line='45')
plt.show()
```

![Screenshot 2024-10-08 131401](https://github.com/user-attachments/assets/84e93d7c-4d28-443c-a3ff-cbc2ac39d585)
```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()
```

![Screenshot 2024-10-08 131409](https://github.com/user-attachments/assets/0cbced58-e8f8-4aa0-a244-a0e6076d57e1)

# RESULT:
  Thus the given data, Feature Encoding, Transformation process and save the data to a file was performed successfully.   

       
