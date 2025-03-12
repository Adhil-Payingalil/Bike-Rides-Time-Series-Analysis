## **Data Preparation (Python using pandas)**

Before working with the data in Tableau,  a series of preprocessing steps was performed with Python.

### **4.1. Data Importing**

```python
import kagglehub
from kagglehub import KaggleDatasetAdapter
import pandas as pd

bikes = kagglehub.load_dataset(
    KaggleDatasetAdapter.PANDAS,
    "hmavrodiev/london-bike-sharing-dataset",
    "london_merged.csv"
)

```

This code snippet imports the necessary libraries and loads the dataset directly from Kaggle using the `kagglehub` library. A pandas DataFrame called `bikes` is created, containing the data from the "london_merged.csv" file.
