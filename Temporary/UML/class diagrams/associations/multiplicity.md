specifies how many occurrences can i class have with an another class during an association.multiplicities are placed on both classes

# different multiplicities

|**Notation**|**Full Syntax**|**Meaning**|**Description**|
|---|---|---|---|
|**`1`**|`1..1`|**Exactly One**|There must be precisely one instance linked.|
|**`0..1`**|`0..1`|**Zero or One**|The link is optional; there can be zero or one instance.|
|**`*`**|`0..*`|**Zero or More**|There can be any number of instances, including none (a collection).|
|**`1..*`**|`1..*`|**One or More**|There must be at least one instance, with no upper limit.|
|**`m..n`**|`m..n`|**Specific Range**|At least $m$ instances and at most $n$ instances (e.g., `2..4`).|
|**`m..*`**|`m..*`|**Open Upper Bound**|At least $m$ instances, with an unlimited maximum (e.g., `5..*`).|
|**`m`**|`m..m`|**Exact Number**|Exactly $m$ instances (e.g., exactly `3`).|

# How to read them

we imaging an arrow pointing to the multiplicity of the other class and read it as this class can have x amount of the other class

## Example

![[image-59.png]]

- a customer can have 0 to multiple different orders
- an order can be placed by 1 customer only
# Example

![[image-60.png]]