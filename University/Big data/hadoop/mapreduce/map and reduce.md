we use map when we want to filter/transform individual items, we use reduce when we want to perform operations on those filtered/transformed items

# Example

```python
%%file wordlengthcount.py
from mrjob.step import MRStep
from mrjob.job import MRJob
class WordLengthCount(MRJob):
	def steps(self):
		return [MRStep(mapper=self.mapper_get_lengths, reducer=self.
			,→reducer_count_lengths)]
	def mapper_get_lengths(self, _, line):
		for word in line.split():
			yield str(len(word)).zfill(2), 1
	def reducer_count_lengths(self, key, values):
		yield key, sum(values)
if __name__ == '__main__':
	WordLengthCount.run()
```

## Map

in this example inside the mapper we use split every line (item) and return length  of the word alongside 1

## Shuffle and sort

![[image-426.png]]
in that example we group all the ones for the words with the same length to end up with something like: 8,[1,1,1,1,1,1,1]

- **Note** if we want to group all the values into a single key we do the following trick
	- yield None,(key,value)
	- shuffle and sort will see that all the keys are None and will groupe all their values into a single list

## Reduce

inside that reduce we take the grouped values from the suffle and reduce section and we sum all the values

- **Example**: 8,[1,1,1,1,1] -> 8,5

