# Expand df column width
#python #pandas

https://re-thought.com/how-to-suppress-scientific-notation-in-pandas/

```python
pd.set_option('display.float_format', lambda x: '%.5f' % x)
```
