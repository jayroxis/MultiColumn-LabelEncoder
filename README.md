# Label Encoder For Multicolumn Pandas Dataframe

Python implementation based on sklearn.
![alt text](https://scikit-learn.org/stable/_static/scikit-learn-logo-small.png)

-----------------------------------------------------------



When handling categorical data, it is very common to utilize the [**LabelEncoder**](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html) provided by [*scikit-learn (sklearn)*](https://scikit-learn.org/stable/).

However, the **LabelEncoder** does not support multi-column *pandas* **DataFrame**. Here I provide a simple implementation of LabelEncoder for multicolumn pandas dataframe based on the [**LabelEncoder**](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html).

-------------------------------------------------------------

## Dependencies

- ***sklearn***: ```pip install --upgrade sklearn```

-------------------------------------------------------------

## Source Code (Python3)

Usage of the **MultiLabelEncoder** is the same as [**LabelEncoder**](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html) but *fit*, *fit_transform* and *inverse_transform* receive [**pandas.DataFrame**](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html).

```python3
from sklearn.preprocessing import LabelEncoder
from collections import defaultdict

# a multi-column label encoder for pandas dataframe 
class MultiLabelEncoder(object):
    def __init__(self):
        super().__init__()
        self.d = defaultdict(LabelEncoder)

    def fit_transform(self, df):
        # Encoding the variable
        return df.apply(lambda x: self.d[x.name].fit_transform(x))

    def fit(self, df):
        df.apply(lambda x: self.d[x.name].fit(x))
        return None

    def transform(self, df):
        return df.apply(lambda x: self.d[x.name].transform(x))

    def inverse_transform(self, df):
        return df.apply(lambda x: self.d[x.name].inverse_transform(x))
```

