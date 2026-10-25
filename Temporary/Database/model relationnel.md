
# Definitions

## Foreign key

### French

Si un attribut est une clé primaire d’une relation 1 et figure dans une
relation 2, toutes les valeurs prises par cet attribut dans la relation 2
doivent obligatoirement exister dans la relation 1.
### english

If an attribute is a primary key of a relation 1 and appears in a relation 2, all values taken by this attribute in relation 2 must necessarily exist in relation 1.

- On appelle degré d’une relation le nombre de ses attributs.

## Domain

### French

Le domaine d’un attribut est l’ensemble, fini ou infini, de ses
valeurs possibles.

### English

The set of allowed values for an attribute (e.g., the domain for `AgePers` is "integer numbers").

## Candidate key

### French 

Une clé candidate d’une relation est un ensemble minimal
des attributs de la relation dont les valeurs identifient à coup sûr une
occurrence.

### english

a candidate key is a set of attributes that uniquely identifies each row in a relation, and is minimal in the sense that no attribute can be removed from the set without losing this uniqueness property. In other words, candidate keys are all the unique attributes that are candidate for becoming the single primary key of a relation.

# Associations

- primary keys are underlined
- foreign keys contains hastag # before their names.

## One to many or One to one

in the case where there is a cardinality of an entity that is larger than the other cardinality we will apply this type of relation which is:

the entity with the smaller cardinality will contain a foreign key referencing the primary key of the entity with the larger cardinality,

this applies to **ALL** associations except :
- 1-1 to 1-1
- many to many associations will be dealt differently, using a junction table,
- n-ary associations

### Examples

![[image-102.png]]
![[image-103.png]]

## Many to Many Associations

for n-ary associations and many to many we turn the association into a junction table where it contains the foreign keys of the primary keys of the associated entities. and also it makes them primary

### Examples

![[image-104.png]]
![[image-105.png]]
![[image-106.png]]

## Note

this also applies to reflexive associations

![[image-107.png]]
![[image-108.png]]

