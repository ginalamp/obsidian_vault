# Get Athena Column Names

#sql #athena #vim


https://docs.aws.amazon.com/athena/latest/ug/show-columns.html

```sql
show columns from database.table
```

# Convert athena columns to list of words
athena column output format -> `var1, var2, var3, ..., varn`


1. In athena, run
```sql
show columns from database.table
```
2. copy output

## Vim Way
1. Paste output in vim
2. Run

```bash
# select all
gg
V
G
# substitute
:'<,'>s/ //g |'<,'>s/\n/, /g
```

## TextEdit Way
1. Paste output in TextEdit
2. Find & Replace
	1. Find -> Pattern -> White Space
	2. Replace -> `, `
3. Remove end comma

# Convert athena columns to list of strings

athena column output format -> `['var1', 'var2', 'var3', 'varn']`
1. In arthena, run
```sql
show columns from database.table
```

2. copy output & paste in vim
3. vim commands

```bash
# select all
gg
V
G
# substitute
:'<,'>s/ //g |'<,'>s/\n/', '/g

# final edits (manual)
# add [] at start and end
# add ' to start
# remove ,' from end
```


