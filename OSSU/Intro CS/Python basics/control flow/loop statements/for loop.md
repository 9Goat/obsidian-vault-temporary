A `for` loop is used to **iterate over a sequence** (like a list, string, tuple, or range) and execute a block of code for each item.

# Syntax

```python
for item in sequence:
    # code block (indented)
    # do something with item
```

# Example

here an example showcasing a loop with a string (sequence)

```python
for letter in "Python":
    print(letter)
```


# Range

range is a function that integer parameters and returns a sequence of numbers depending on those parameters, range accepts 3 parameters which are the following:

**range(start,end,step)**

- **start(optional)**: determines the starting index of the sequence
- **end(REQUIRED)**: determines the ending index of the sequence
- **step(optional)**: determines the step between each sequence number
	- **Note**: if negative the sequence will be reversed(and we will have to reverse the order of the start and end. see the example for more clarification)

## Example

```python
print(list(range(10)))  
print(list(range(1, 10)))  
print(list(range(1, 10, 2)))  
print(list(range(10, 1, -2)))
```

