# Python Scripting
<!--
## Data Types

### Strings

+ `"string".title()` to capitalize the first letter and lowercase the rest.
-->
## Data Structures

### Lists

+ List in Python are arrays in other languages. 
+ Formed with `[]` brackets with comma seperated values.
+ Zero based index access to values.
	+ `len(list)` returns the length of a list.
	+ `list[0]` get the first element.
	+ `list[len(list) - 1] to get the last element.
	+ `list[-1]` get the last element of the list.
+ `list[2] = "value"` reassign a value.
+ `list.append("value")` add element to the end of the list.
	+ `list.insert(n, "value")` insert value into index n.
	+ `list.pop()` with no arguments will remove the last item of the list
		+ `list.pop(n)` will remove element at index n.
	+ `variable = list.pop()` will remove an element and assign it to the variable
+ `list.remove("value")` remove element by value literal.
+ `list.sort()` sort ascending order, will change the array
	+ `sorted(list)` sort ascending order without changing the array.

#### Slice

+ `:` in array brackets creates a slice where a starting and ending position is specified, exclusive
	+ `list[0:1]` - gets values from index 0 to index 1 exclusive, therefore returning value at index 0.
	+ `list[1:5]` - gets value from index 1 to 4
	+ `list[2:] - get every item starting from index 2 to the upper bound of list
	+ `list[2:-1]` - get every item from index 2 to upper bound less 1.
	+ `list[:5]` - get every element before index 5 exclusive (not including index 5)

### Ranges

+ `range()` - Create a range between two numbers, exclusive.
	+ `range(0, 5)` creats a range between 0 and 4

## Looping

+ Looping a list

```python

for item in items:
	print(item)
```

+ Looping a range

```python
for i in range(0,5):
	print(i)

for item in range(0, len(items) - 1)
	print(items[item])
```

+ Looping a slice

```python
# print from index 2 to 10
for item in items[2:10]:
	print(item)

# If the total length is unknown
for item in items[2:]:
	print (item)

# Limit iteration
for item in items[:10]:
	print (item)
```
