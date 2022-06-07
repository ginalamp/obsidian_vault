# Fuzzy Logic - Approximate String Matching

#python #datascience #string 

[Toward Data Science: Fuzzy String Matching in Python](https://towardsdatascience.com/fuzzy-string-matching-in-python-68f240d910fe)
[Towards Data Science: FuzzyWuzzy - How to measure string distance in Python](https://towardsdatascience.com/fuzzywuzzy-how-to-measure-string-distance-on-python-4e8852d7c18f)

# Fuzzy String Matching Theory

[Fuzzy logic](https://en.wikipedia.org/wiki/Fuzzy_logic) is a form of multi-valued logic that deals with reasoning that is approximate rather than fixed and exact. Fuzzy logic values range between 1 and 0. i.e the value may range from completely true to completely false.

[Fuzzy String Matching](https://en.wikipedia.org/wiki/Approximate_string_matching), also known as Approximate String Matching, is the process of finding strings that approximately match a pattern.


## Levenshtein Distance
* it counts how many substitutions are needed, given a string _u_, to transform it into _v_.
	* * the minimum amount of these substitution operations that need to be done to _u_ in order to turn it into _v,_ correspond to the Levenshtein distance between those two strings.
* for this method, a substitution is defined as:
	*  Erasing a character.
	* Adding one.
	* Replacing a character with another one.
* the Levenshtein distance is **at most the length of the longest string**
	* replace all characters in the shorter one with the first part of the longer one, and then add the remaining ones

# Python Library: Fuzzywuzzy
Uses Levenshtein Distance

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

#Output  
> [("Men's 3000 meter steeplechase", 100),  
> ('mens 3000 meter SteepleChase', 95),  
> ('3000m STEEPLECHASE MENS', 85),  
> ('3000m Steeplechase', 77)]
```

### ExtractOne
* extract, but returns only the string with the highest simularity score

```python
process.extractOne("Men's 3000 Meter Steeplechase", choices,
				   scorer=fuzz.token_sort_ratio)
#Output  
> ("Men's 3000 meter steeplechase", 100)
```





