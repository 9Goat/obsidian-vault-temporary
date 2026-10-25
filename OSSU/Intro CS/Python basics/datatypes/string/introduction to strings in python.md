#  Syntax 

string in python are represented by their double quotation marks **`"string"`**

```python
x = "hello world"
print(x)
```

# operations on python

strings do allow operations to be made on them, most notably:

- multiplying string by integers(not floats)
- adding strings to each other (concatenation)

```python
x = "hello"  
y = x * 5  
z = x + " world"  
print(y)  
print(z)
```

#  Indexing

Python uses **zero-based indexing**, meaning the first character is at index `0`:

```python
text = "Python"

print(text[0])   # 'P' - first character
print(text[1])   # 'y'
print(text[5])   # 'n' - last character
```

## negative indexes

You can also count from the end using negative indices:

```python
text = "Python"

print(text[-1])  # 'n' - last character
print(text[-2])  # 'o' - second to last
print(text[-6])  # 'P' - first character
```

## slicing

we can also use indexes to slice a string into a substring

```python
text = "Python"

print(text[0:3])   # 'Pyt' - characters from index 0 to 2 (end is exclusive)
print(text[:3])    # 'Pyt' - same as above
print(text[3:])    # 'hon' - from index 3 to end
print(text[:])     # 'Python' - entire string
print(text[::2])   # 'Pto' - every 2nd character
print(text[::-1])  # 'nohtyP' - reversed string
```

## Notes

- you cannot inside values to indexes
	- `python text[0] = 'J'  # ❌ TypeError: 'str' object does not support item assignment`
- **Valid range**: `-len(text)` to `len(text) - 1` trying to access an index outside that range will result in an error


