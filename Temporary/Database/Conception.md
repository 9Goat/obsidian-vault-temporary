# Definitions

## Occurrences / instances

- **French**:Une occurrence d’entité est un objet, une chose concrète ou abstraite qui peut être reconnue distinctement et qui est caractérisée par son unicité.
- **English**:An entity occurrence is an object, a concrete or abstract thing that can be distinctly recognized and is characterized by its uniqueness.

## Entite / Entities

- **French**:Un type - entité ou ent ité désigne un ensemble d’entités qui possèdent une sémantique et des propriétés communes.
- **English**:Entity - An entity type or entity designates a set of entities that have common semantics and properties.

## Attribute /Valeur

![[image-2.png]]

- **French**:Un attribut (ou une propriété) est une caractéristique associée à une entité ou à une association.
- **English**: An attribute (or property) is a characteristic associated with an entity or association

- **French**:
	- Au niveau d’une entité ou une association, chaque attribut possède un domaine qui définit l’ensemble des valeurs possibles qui peuvent être choisies pour lui (entier, chaîne de caractères, booléen, . . .).
	- Au niveau d’une occurrence, chaque attribut possède une valeur compatible avec son domaine.
- **English**:
	- At the entity or association level, each attribute has a domain that defines the set of possible values that can be chosen for it (integer, string, boolean, etc.)
	- At the occurrence level, each attribute has a value compatible with its domain.

## Identifier or Key

![[image-3.png]]

- **French**:Un identifiant (ou clé) d’une entité ou d’une association est constitué par un ou plusieurs de ses attributs q ui doivent avoir une valeur unique pour chaque entité ou association de ce type.
- **English**: An identifier (or key) of an entity or association consists of one or more of its attributes which must have a unique value for each entity or association of that type.

***an identifier/key is represented by an underline inside an entity***

## Association / Relationship

![[image-4.png]]
![[image-6.png]]

- **French**:Une instance d’association (ou de relation) est un lien entre plusieurs occurrence d’entités
- **English**: An association (or relationship) instance is a link between several occurrences of entities.
	- **Example:** In a `Student` entity and a `Course` entity, the specific fact that "John Doe is enrolled in Computer Science 101" is an instance of an association.

- **French**:une association (ou une relation) désigne un ensemble de relations qui possèdent les mêmes caractéristiques. Une association décrit un lien entre plusieurs occurrence d’entités..
- **English**: An association (or relationship) refers to a set of relationships that have the same characteristics. An association describes a link between multiple occurrences of entities.
	- **Example:** "Enrollment" is an association between the `Student` entity and the `Course` entity. It describes the general concept of students taking courses

- **French**: `participant` Les entités intervenant dans une association sont appelés les participants de cette association.
- **English**: Participant - The entities involved in an association are called the participants of that association

- **French**: `collection` - L’ensemble des participants d’une association est appelé la collection de cette association
- **English**: collection - The set of participants in an association is called the collection of that association.

- **French**:`dimension` ou arité d’une association - La dim ension, ou l’arité d’une association est le nombre d’entités contenu dans la collection.
- **English**: Dimension or arity of an association - The dimension of an association is the number of entities contained in the collection.

- **French**:`Type association réflexif` - Un type - association est qualifié de réflexif quand il matérialise une relation entre un type - entité et lui- même.
- **English**: qualified as reflexive when it materializes a relationship between an entity-type and itself.(basically a relationship that connects an **entity to itself**)
![[image-9.png|Association reflexive]]
### Association n-aire (N>2)
![[image-10.png]]
## Cardinalite

![[image-8.png]]

- **French**:`La cardinalité` d’une patte reliant une association et une entité précise le nombre de fois minimal et maximal d’interventions d’une occurrence d’entité d’une entité dans une association.
- **English**: The cardinality is the connection between an association and an entity that specifies the minimum and maximum number of times an entity occurrence of an entity may occur in an association.

### Types of cardinality

- **`0.1`**: An occurrence of the entity type can exist while being involved in no association and can be involved in at most one association.
- **`0,n`**: this is the most open cardinality; an occurrence of the type entity may exist while being involved in no association and may be involved, without limitation, in multiple associations.
- **`1.1`**: An occurrence of the entity-type can only exist if it is involved in exactly (at least and at most) one association.
- **`1,n`**: an occurrence of the entity type can only exist if it is involved in at least one association.

## Preimer form normalle (1FN)

- **French**:Une entité ou une ass ociation est en première forme normale si tous ses attributs sont élémentaires, c’est -à- dire non décomposables.
- **English**: An entity or association is in first normal form if all its attributes are elementary, that is, not decomposable.(it means that no attribute should be able to hold more than a single value)
	- **Example**: if we have an entity called **`person`** which contains an attribut that can contain more than 1 value like **`phoneNumbers`** then to make it **1FN** we have to create an association called **`contacts`** to hold those multiple phone numbers

## Deuxiem form normalle (2FN)

- **French**:Une entité ou une association est en deuxième forme normale si, et seulement si, il est en première forme normale et si tout attribut n’appartenant pas à la clé, dépend de la totalité de cette clé.
- **English**: An entity or association is in second normal form if, and only if, it is in first normal form and if every attribute not belonging to the key depends on the whole of this key.(meaning all attributes that are **NOT** primary keys **MUST** be related and depend on **ALL** primary keys of that entity)
	- **Example**, imagine a `Project_Assignments` table with a composite primary key of `(DeveloperID, ProjectID)` that includes a non-key attribute `Hourly_Rate`. Since the `Hourly_Rate` depends only on the `DeveloperID` and not the `ProjectID`, this is a partial dependency. To normalize it, you must split the data. You would create a new `Developers` table to store the `DeveloperID` and `Hourly_Rate` (since the rate is dependent only on the developer), and an `Assignments` table to manage the many-to-many relationship between developers and projects
## Troiseme form nomalle (3FN)

- **French**:Une entité ou une association est en troisième forme normale si, et seulement si, il est en deuxième forme normale et si tous ses attributs dépendent directement de sa clé et pas d’autres attributs.
- **English**: An entity or association is in third normal form if, and only if, it is in second normal form and all of its attributes depend directly on its key and not on other attributes.
	- **Example**: if a table has `ProductID` as the primary key and includes `SupplierID` and `SupplierName`, it violates 3NF because `SupplierName` depends on `SupplierID`, not directly on `ProductID`. To fix this, you would move the `SupplierID` and `SupplierName` to a separate `Suppliers` table, leaving only the `SupplierID` in the original table to link back to the supplier information
## Forme normale de Boyce-Codd (BCNF)

- **French**:Une entité ou une association est en forme normale de Boyce - Codd si, et seulement si, il est en troisième forme normale et si aucun attribut faisant partie de la clé dépend d’un attribut ne faisant pas partie de la clé.
- **English**: An entity or association is in Boyce-Codd normal form if, and only if, it is in third normal form and no attribute in the key depends on an attribute not in the key.
	- **Example**:in a table storing a student's tutor and subject, where a student can have multiple tutors but a specific tutor only teaches one subject, a dependency like `(TutorID) -> (Subject)` would violate BCNF if the primary key is `(StudentID, Subject)`, as `(TutorID)` is not a superkey. To fix this, you'd create a separate `Tutors` table to store `TutorID` and `Subject` and link it back to the original table.

# Entity rules

1. an attribute cannot be shared by multiple entities
	- if we have an attribute called **`studentName`** it shouldnt be shared across other entities especially those that are not related to the **`student`** entity
 2. do not store attributes that can be calculated by other attributes 
	 - for example if we have the attribute **`birthDate`** we should not create an attribute called **`age`** since we can calculate the age using  **`birthDate`**
3. entities must represent a concept and its attributs must be related to that concept 
	- for example we can create an entity called **`person`** and its attribute must resemble a person meaning **`monitureSize`** should NOT be an attribute to the entity person
4. every **entity** must have at least one unique **identifier**, which can be composed of one or more **attributes**.
	- this is mandatory to distinguish entities from others
5. An attribute can be placed in an association only when it depends on all entities linked by the association.
	- Look at [[Conception#Association / Relationship|Assocation]] example
6. The expression of cardinality is mandatory for each connection of an association.
7. In an entity-relationship model, the name of an entity, association or attribute must be unique.
	- for example if we have an entity called **`Student`** and an entity called **`Teacher`** which both have an attribute called **`Fullname`** then we have to rename that attribute to **`Student Fullname`** and **`Teacher Fullname`** to avoid repetition.
8. if we have multiple attributes that share the same topic we can compose them into an entity and a relationships to simplify it

## Example of rule 8

![[image-11.png]]

9. when we have multiple entities that share similar attributes and **CAN** be resembled into a general entity then we can to merge them together as long as it doesnt ruin any connection with other entities

## Example of rule 9

![[image-12.png]]

10. When the cardinalities of an association are all 1, 1 means that the association should not exist. and we should merge them together

## Example of rule 10

![[image-13.png]]

11. avoid redundant association
	- for example instead of having 2 connections for **`paying`** and **`receiving`** we can just have a single connection between the **`client`** and **`provider`** called **`transaction`** 

