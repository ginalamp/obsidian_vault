# Fuzzy Logic - Approximate String Matching

#python #datascience #string 

[Toward Data Science: Fuzzy String Matching in Python](https://towardsdatascience.com/fuzzy-string-matching-in-python-68f240d910fe)
[Towards Data Science: FuzzyWuzzy - How to measure string distance in Python](https://towardsdatascience.com/fuzzywuzzy-how-to-measure-string-distance-on-python-4e8852d7c18f)

# Fuzzy String Matching Theory

[Fuzzy logic](https://en.wikipedia.org/wiki/Fuzzy_logic) is a form of multi-valued logic that deals with reasoning that is approximate rather than fixed and exact. Fuzzy logic values range between 1 and 0. i.e the value may range from completely true to completely false.

[Fuzzy String Matching](https://en.wikipedia.org/wiki/Approximate_string_matching), also known as Approximate String Matching, is the process of finding strings that approximately match a pattern.


## Levenshtein Distance
* it counts how many substitutions are needed, given a string _u_, to transform it into _v_.
	* the minimum amount of these substitution operations that need to be done to _u_ in order to turn it into _v,_ correspond to the Levenshtein distance between those two strings.
* for this method, a substitution is defined as:
	*  Erasing a character.
	* Adding one.
	* Replacing a character with another one.
* the Levenshtein distance is **at most the length of the longest string**
	* replace all characters in the shorter one with the first part of the longer one, and then add the remaining ones

# Python Library: Fuzzywuzzy
[fuzzywuzzy](https://pypi.org/project/fuzzywuzzy/) uses Levenshtein Distance and is built on top of the [difflib](https://docs.python.org/3/library/difflib.html) library
* The FuzzyWuzzy library is built on top of `difflib` library and `python-Levenshtein` is used for speed.

```shell
pip3 install fuzzywuzzy python-Levenshtein
```

```python
from fuzzywuzzy import fuzz  
from fuzzywuzzy import process
```

## Functions
[Stack Overflow: When to use which fuzz function to compare 2 strings](https://stackoverflow.com/questions/31806695/when-to-use-which-fuzz-function-to-compare-2-strings)

[Towards Data Science: String Matching with FuzzyWuzzy](https://towardsdatascience.com/string-matching-with-fuzzywuzzy-e982c61f8a84)

Similarity Score will always return a number between 0 and 100

### Ratio
* could be a fuzzy replacement to the _equals_ string method
* fails for strings that are similar, but whose words appear in a different order
```python
fuzz.ratio("NEW YORK METS", "NEW YORK MEATS")
> 96
```

### Partial Ratio
* could be a fuzzy replacement to the _contains_ string method
	* attempts to account for partial string matches better
* Calls `ratio` using the **shortest string** (length n) against all n-length substrings of the larger string and returns the highest score
* fails for strings that are similar, but whose words appear in a different order
```python
fuzz.ratio("YANKEES", "NEW YORK YANKEES")
> 60
fuzz.partial_ratio("YANKEES", "NEW YORK YANKEES")
> 100
```

### Token Sort Ratio
* account for similar strings that are out of order
	* Calls `ratio` on both strings after sorting the tokens in each string
* divides strings into words, then joins those again alphanumerically, before calling the regular ratio on them

```python
fuzz.ratio("New York Mets vs Atlanta Braves", "Atlanta Braves vs New York Mets")
> 45
fuzz.partial_ratio("New York Mets vs Atlanta Braves", "Atlanta Braves vs New York Mets")
> 45
fuzz.token_sort_ratio("New York Mets vs Atlanta Braves", "Atlanta Braves vs New York Mets")
> 100
```

### Token Set Ratio
* similar to `token_sort_ratio`, except it takes out the common tokens before calling `ratio`
	* It removes the words that do not match and then calculates the simularity between the new strings
* separates each string into words, turns both lists into sets (discarding repeated words) and then sorts those before doing the ratio.

```python
fuzz.ratio("mariners vs angels", "los angeles angels of anaheim at seattle mariners")
> 36
fuzz.partial_ratio("mariners vs angels", "los angeles angels of anaheim at seattle mariners")
> 61
fuzz.token_sort_ratio("mariners vs angels", "los angeles angels of anaheim at seattle mariners")
> 51
fuzz.token_set_ratio("mariners vs angels", "los angeles angels of anaheim at seattle mariners")
> 91
```

### Extract
* returns the strings along with a similarity score out of a vector of strings

```python
choices = ["3000m Steeplechase", "Men's 3000 meter steeplechase",                    "3000m STEEPLECHASE MENS", "mens 3000 meter SteepleChase"]

process.extract("Men's 3000 Meter Steeplechase", choices,/
				scorer=fuzz.token_sort_ratio)

> [("Men's 3000 meter steeplechase", 100),  
	('mens 3000 meter SteepleChase', 95),  
	('3000m STEEPLECHASE MENS', 85),  
	('3000m Steeplechase', 77)]
```

### ExtractOne
* extract, but returns only the string with the highest simularity score

```python
process.extractOne("Men's 3000 Meter Steeplechase", choices,
				   scorer=fuzz.token_sort_ratio)
> ("Men's 3000 meter steeplechase", 100)
```


## Merging DataFrames On Match
[Towards Data Science: String Matching with FuzzyWuzzy](https://towardsdatascience.com/string-matching-with-fuzzywuzzy-e982c61f8a84)
```python
# Casting the name column of both dataframes into lists
df1_names = list(df_1.name.unique())  
df2_names = list(df_2.name.unique())  

# Defining a function to return the match and similarity score of the fuzz.ratio() scorer. The function will take in a term(name), list of terms(list_names), and a minimum similarity score(min_score) to return the match.
def match_names(name, list_names, min_score=0):  
    max_score = -1  
    max_name = ''  
    for x in list_names:  
        score = fuzz.ratio(name, x)  
        if (score > min_score) & (score > max_score):  
            max_name = x  
            max_score = score  
    return (max_name, max_score)  

# For loop to create a list of tuples with the first value being the name from the second dataframe (name to replace) and the second value from the first dataframe (string replacing the name value). Then, casting the list of tuples as a dictionary.
names = []  
for x in doping_names:  
    match = match_names(x, athlete_names, 75)  
    if match[1] >= 75:  
        name = ('(' + str(x), str(match[0]) + ')')  
        names.append(name)  
name_dict = dict(names)  
name_dict

# Using the dictionary to replace the keys with the values in the 'name' column for the second dataframe
df_2.name = df_2.name.replace(name_dict)

# match on fuzzy 'name'
combined_dataframe = pd.merge(df_1, df_2, how='left', on='name')
```

# Fuzzywuzzy on Dataframes
[How to do Fuzzy Matching on Pandas Dataframe Column Using Python?](https://www.geeksforgeeks.org/how-to-do-fuzzy-matching-on-pandas-dataframe-column-using-python/)

```python
import pandas as pd
from fuzzywuzzy import fuzz
from fuzzywuzzy import process

# creating the dictionaries
dict1 = {'name': ["aparna", "pankaj", "sudhir",
				"Geeku", "geeks for geeks"]}

dict2 = {'name': ["aparn", "arup", "Pankaj",
				"for geeks geeks", "sudhir c",
				"Geek"]}

# converting to pandas dataframes
dframe1 = pd.DataFrame(dict1)
dframe2 = pd.DataFrame(dict2)

# empty lists for storing the matches later
mat1 = []
mat2 = []
p = []

# printing the pandas dataframes
print("First dataframe:\n", dframe1,
	"\nSecond dataframe:\n", dframe2)

# converting dataframe column to list of elements to do fuzzy matching
list1 = dframe1['name'].tolist()
list2 = dframe2['name'].tolist()

# taking the threshold as 80
threshold = 80

# iterating through list1 to extract it's closest match from list2
for i in list1:
	mat1.append(process.extractOne(
	i, list2, scorer=fuzz.token_sort_ratio))
dframe1['matches'] = mat1

# iterating through the closest matches to filter out the maximum closest match
for j in dframe1['matches']:
	if j[1] >= threshold:
		p.append(j[0])
	mat2.append(",".join(p))
	p = []


# storing the resultant matches back to dframe1
dframe1['matches'] = mat2
print("\nDataFrame after Fuzzy matching using fuzz.token_sort_ratio:")
dframe1
```

# FuzzyWuzzy with PySpark

* [Create new column with fuzzy-score across two string columns in the same dataframe](https://stackoverflow.com/questions/65325782/create-new-column-with-fuzzy-score-across-two-string-columns-in-the-same-datafra)
* [Faster String Matching Using Fuzzy Wuzzy and Spark/Databricks](https://medium.com/@prashantsingh2026/faster-string-matching-using-fuzzy-wuzzy-and-spark-databricks-8dc589635151)

