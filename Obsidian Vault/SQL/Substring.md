# Substring

#sql #athena 

https://prestodb.io/docs/current/functions/string.html


```sql
substr(_string_, _start_) → varchar

-- Returns the rest of `string` from the starting position `start`. Positions start with `1`. A negative starting position is interpreted as being relative to the end of the string.

substr(_string_, _start_, _length_) → varchar

-- Returns a substring from `string` of length `length` from the starting position `start`. Positions start with `1`. A negative starting position is interpreted as being relative to the end of the string.
```