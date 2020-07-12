# Label Encoder For Multicolumn Pandas Dataframe

-----------------------------------------------------------
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

