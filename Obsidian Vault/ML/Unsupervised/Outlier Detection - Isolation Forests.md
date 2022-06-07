# Isolation Forests with Statistical Rules
#ml #python #outlierdetection #unsupervised
[Anomaly Detection : Isolation Forest with Statistical Rules](https://towardsdatascience.com/isolation-forest-with-statistical-rules-4dd27dad2da9)

## Definition
Isolation forest works on the principle of the decision tree algorithm. It isolates the outliers by randomly selecting a feature from the given set of features and then randomly selecting a split value between the maximum and minimum values of the selected feature. This random partitioning of features will produce smaller paths in trees for the anomalous data values and distinguish them from the normal set of the data.

BUT! We want to add statistical rules, as we don't want to have a set percentage points of the data to be anomalous.


## Python Library
```python
from sklearn.ensemble import IsolationForest
```

### Example setup
```python
clf = IsolationForest(n_estimators=10, max_samples='auto', contamination=float(.04), \
                        max_features=1.0, bootstrap=False, n_jobs=-1, random_state=42, verbose=0)
clf.fit(df[['<features>']].values)

df['scores'] = clf.decision_function(df[['<features>']].values)
df['anomaly'] = clf.predict(df[['<features>']].values)

df.loc[df['anomaly'] == 1,'anomaly'] = 0
df.loc[df['anomaly'] == -1,'anomaly'] = 1
df['anomaly'].value_counts()
```

### Hyperparameters
**Maximum Number Features:** The default value of max features is 1. The maximum number of features is the number of features to draw from the total features to train each tree.

**Maximum Number of Samples:** Indicates the number of samples to be drawn to train each tree. If this value is more than the number of samples provided, all samples will be used.

**Contamination:** This is the expected proportion of outliers in the dataset and is quite sensitive. This is used when fitting to define the threshold on the scores of the samples.

**Count of Estimators:** It is an optional parameter with a default value equal to 100. This refers to the number of trees that will get built in the forest.

### Output
Scores: `decision_function()`

These scores are used to determine whether the item is an anomaly or not.


## Statistical Rules
Inter-quartile range of scores.

```python
def iqr_bounds(scores,k=1.5):
	'''
		Get the inter-quartile bounds for the isolation forest anomaly scores.

		Args:
			scores: scores produced by the Isolation forest algorithm
			k: iqr multiplier
		Returns:
            lower_bound: lower bound for the isolation forest score to be an anomaly
            upper_bound: upper bound for the isolation forest score to be an anomaly
			
	'''
    q1 = scores.quantile(0.25)  
    q3 = scores.quantile(0.75)  
    iqr = q3 - q1  
    lower_bound=(q1 - k * iqr)  
    upper_bound=(q3 + k * iqr)
    print("lower bound: {}\nUpper bound: {}".format(lower_bound, upper_bound))
    
    return lower_bound, upper_bound
    
lower_bound, upper_bound = iqr_bounds(df['scores'], k=2)
df['anomaly'] = 0  
df['anomaly'] = (df['scores'] < lower_bound) | (df['scores'] > upper_bound)  
df['anomaly'] = df['anomaly'].astype(int)  
```
