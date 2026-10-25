
# defining the methods

```python
from mrjob.step import MRStep
from mrjob.job import MRJob
class WordCount(MRJob):
    def steps(self):
        return [MRStep(mapper=self.mapper_get_words, 
		        reducer=self.reducer_count_words),
                MRStep(reducer=self.reducer_tri)]
```

# zfilld

zfill is a command that adds multiple zeros infront of a string number, to make it functional we first need to transform the number into string and then we specify how many zeros we want to add

## Example

```python
count = 40
result = str(count).zfill(6)
```

- result will be :"000040" the digit 6 represents the total length of the string 