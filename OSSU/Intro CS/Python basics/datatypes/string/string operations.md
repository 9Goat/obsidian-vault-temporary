in this page we will discuss, the most important and notable string operations methods(not all of them), ill be sharing 20 methods:


## 1. `len()`
**Description:** A function used to determine the total number of characters in a string.

```python
text = "Hello, World!"
print(len(text))
```
**Output:** `13`


## 2. `find()`
**Description:** Returns the index of the first occurrence of a specific character or substring. Returns `-1` if not found.

```python
text = "Python is awesome"
print(text.find("is"))
print(text.find("Java"))
```
**Output:**
```
7
-1
```


## 3. `rfind()`
**Description:** Returns the index of the last occurrence of a specified character or substring. Returns `-1` if not found.

```python
text = "banana"
print(text.rfind("a"))
print(text.rfind("n"))
```
**Output:**
```
5
4
```


## 4. `capitalize()`
**Description:** Capitalizes only the first letter of the entire string and makes all other characters lowercase.

```python
text = "hello WORLD"
print(text.capitalize())
```
**Output:** `Hello world`



## 5. `upper()`
**Description:** Converts all characters in a string to uppercase.

```python
text = "python programming"
print(text.upper())
```
**Output:** `PYTHON PROGRAMMING`



## 6. `lower()`
**Description:** Converts all characters in a string to lowercase.

```python
text = "PYTHON PROGRAMMING"
print(text.lower())
```
**Output:** `python programming`



## 7. `isdigit()`
**Description:** Returns a boolean indicating if the string contains only numeric digits.

```python
print("12345".isdigit())
print("123.45".isdigit())
print("123abc".isdigit())
```
**Output:**
```
True
False
False
```



## 8. `isalpha()`
**Description:** Returns a boolean indicating if the string consists solely of alphabetical characters (no spaces, digits, or special characters).

```python
print("Hello".isalpha())
print("Hello World".isalpha())
print("Hello123".isalpha())
```
**Output:**
```
True
False
False
```



## 9. `count()`
**Description:** Returns the total number of times a specific character or substring appears in a string.

```python
text = "banana"
print(text.count("a"))
print(text.count("an"))
```
**Output:**
```
3
2
```



## 10. `replace()`
Substitutes occurrences of a specified character or substring with a new character or string. Returns a new string.

```python
text = "I like cats"
print(text.replace("cats", "dogs"))
print(text.replace(" ", ""))
```
**Output:**
```
I like dogs
Ilikecats
```


## 11. `strip()`
Removes leading and trailing whitespace (or specified characters).

```python
text = "  Hello World  "
print(text.strip())      # 'Hello World'
print(text.strip(' '))   # 'Hello World'
```

## 12. `split()`
Splits a string into a list of substrings based on a delimiter.

```python
text = "apple,banana,orange"
print(text.split(','))   # ['apple', 'banana', 'orange']
```

## 13. `join()`
Concatenates a list of strings into a single string with a specified separator.

```python
fruits = ['apple', 'banana', 'orange']
print(', '.join(fruits))  # 'apple, banana, orange'
```

## 14. `startswith()`
Checks if a string starts with a specified prefix (returns boolean).

```python
text = "Python is great"
print(text.startswith("Python"))  # True
print(text.startswith("Java"))    # False
```

## 15. `endswith()`
Checks if a string ends with a specified suffix (returns boolean).

```python
filename = "document.pdf"
print(filename.endswith(".pdf"))  # True
print(filename.endswith(".txt"))  # False
```

## 16. `title()`
Capitalizes the first letter of each word in a string.

```python
text = "hello world python"
print(text.title())  # 'Hello World Python'
```

## 17. `isalnum()`
Checks if all characters in the string are alphanumeric (letters or digits).

```python
print("Hello123".isalnum())   # True
print("Hello 123".isalnum())  # False (contains space)
print("Hello!".isalnum())     # False (contains punctuation)
```

## 18. `index()`
Similar to `find()`, but raises a `ValueError` if the substring is not found.

```python
text = "Python programming"
print(text.index("programming"))  # 7
print(text.index("Java"))         # ValueError: substring not found
```

## 19. `zfill()`
Pads a string with zeros on the left to fill a specified width.

```python
number = "42"
print(number.zfill(5))  # '00042'
```

## 20. `format()`
Formats a string by replacing placeholders with values.

```python
name = "Alice"
age = 25
print("My name is {} and I'm {} years old.".format(name, age))
# 'My name is Alice and I'm 25 years old.'
```

### F strings

to achieve the same results as format we can use f strings, by simply applying this syntax

```python
name = "Alice"
age = 25

# Old way using format()
print("My name is {} and I'm {} years old.".format(name, age))

# F-string way (much cleaner!)
print(f"My name is {name} and I'm {age} years old.")
```

