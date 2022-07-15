# Groupby Multi-index nlargest on 2nd index
#pandas #python

https://stackoverflow.com/questions/41722785/returning-top-n-values-for-group-multiindex-in-pandas

Get the top 3 stores by total sales per banner
```python
df.groupby(["Store Type", "Store Name"])["Total sales"].sum().groupby(level='Store Type').nlargest(3).reset_index(level=0)
```
