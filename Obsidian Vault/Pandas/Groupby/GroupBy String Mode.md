# Groupby String Mode
#python #pandas

Get the most frequently occuring string in a groupby aggregate

[GroupBy pandas DataFrame and select most common value](https://stackoverflow.com/questions/15222754/groupby-pandas-dataframe-and-select-most-common-value)
* `.agg(pd.Series.mode)`


```python
source.groupby(['Country','City'])['Short name'].agg(pd.Series.mode)
```