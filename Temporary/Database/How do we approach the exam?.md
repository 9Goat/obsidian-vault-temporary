here is an example problem that we are going to be using to explain how to find the information we need to draw the database representation

![[image-36.png]]

# How to extract entities

**Entities** are the main objects, concepts, or things about which you need to store information. They are typically represented by **nouns that can describe a certain object** in the text. When  a noun appears many times in a text expect it to be an entity (write all words we suspect to be entities the first time we read it afterwards read it and and remove that is not an entity)

| **Text Description**                             | **Entity Identified**    | **Rationale**                                                                                                                                                              |
| ------------------------------------------------ | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Un film** est réalisé par...                   | **Film**                 | A core object of the system.                                                                                                                                               |
| Un réalisateur peut lui-même être **un acteur**. | **Artiste**              | This entity is often a combined one (Artiste/Personne) to cover both **Réalisateur** (Director) and **Acteur** (Actor), as the text suggests a director _can be_ an actor. |
| Une **salle** a une capacité...                  | **Salle** (Theater/Room) | Where films are projected.                                                                                                                                                 |

# How to extract attributes

**Attributes** are the properties or characteristics that describe an entity typical fond when describing an entity.  (places the attributes next to what we suspect to be an entity by separating them with slashes)

| **Entity**  | **Text Description Source**                                                            | **Attributes Identified**                          | **Primary Key (Underlined)**                                                              |
| ----------- | -------------------------------------------------------------------------------------- | -------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Film**    | Un film est réalisé... a une durée en minute; il est classé dans un genre particulier. | $\underline{\text{CodeF}}$, TitreF, DureeF, GenreF | $\underline{\text{CodeF}}$ (A unique identifier, often inferred if not explicitly named). |
| **Artiste** | Un acteur joue... il réside dans une seule ville.                                      | $\underline{\text{CodeArt}}$, NomArt, VilleArt     | $\underline{\text{CodeArt}}$                                                              |
| **Salle**   | Une salle a une capacité en nombre de personnes ; elle est située dans une ville.      | $\underline{\text{NumS}}$, NomS, CapacitéS, VilleS | $\underline{\text{NumS}}$                                                                 |

# How to extract associations

**Relationships** are the associations between two or more entities. They are often represented by **verbs** or verbal phrases. (write an arrow between entities to showcase that we think is an association)

|**Text Description Source**|**Relationship Identified**|**Involved Entities**|
|---|---|---|
|Un film est **réalisé** par un seul réalisateur.|**Réaliser** (Direct)|Film and Artiste (as Réalisateur)|
|Un acteur **joue** dans plusieurs films.|**Jouer** (Act)|Artiste (as Acteur) and Film|
|Un film est **projeté** dans plusieurs salles à certaines date et heure.|**Projeter** (Project)|Film and Salle|

to name associations we can use verbs like: etre faire and avoir

| **Verb Type**         | **Example Association** | **French Name**        | **English Translation**              |
| --------------------- | ----------------------- | ---------------------- | ------------------------------------ |
| **Possession/Link**   | Client and Commande     | **Avoir**              | (Client) _has_ (Commande)            |
| **Creation/Function** | Professeur and Cours    | **Donner** / **Faire** | (Professeur) _gives_ (Cours)         |
| **Membership/State**  | Étudiant and Classe     | **Être inscrit**       | (Étudiant) _is enrolled in_ (Classe) |
| **Location**          | Salarié and Local       | **Être affecté à**     | (Salarié) _is assigned to_ (Local)   |
# Extract cordinalities

corndinalities are often shown by using terms suchs as 'un' or 'plusieurs' they are very commonly found near the associations text (underline what we suspect to make a cordinality)

| **Relationship** | **Entities**                   | **Text Description Source**                                                                          | **Cardinalities (Min, Max)**                 | **Rationale**                                                                                            |
| ---------------- | ------------------------------ | ---------------------------------------------------------------------------------------------------- | -------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Réaliser**     | Film $\leftrightarrow$ Artiste | _Un film_ est réalisé par _un seul réalisateur_. Un _réalisateur_ peut jouer dans _plusieurs films_. | Film $\to$ Artiste: $\mathbf{(1, 1)}$        | A film must have exactly one director.                                                                   |
|                  |                                |                                                                                                      | Artiste $\to$ Film: $\mathbf{(0, \text{n})}$ | A director can direct zero or many films.                                                                |
| **Jouer**        | Artiste $\leftrightarrow$ Film | _Un acteur_ **joue** dans _plusieurs films_. Un _film_ peut avoir _plusieurs acteurs_.               | Artiste $\to$ Film: $\mathbf{(0, \text{n})}$ | An artist can act in zero or many films.                                                                 |
|                  |                                |                                                                                                      | Film $\to$ Artiste: $\mathbf{(0, \text{n})}$ | A film can have zero or many actors.                                                                     |
| **Projeter**     | Film $\leftrightarrow$ Salle   | _Un film_ est **projeté** dans _plusieurs salles_. _Une salle_ projette _plusieurs films_.           | Film $\to$ Salle: $\mathbf{(1, \text{n})}$   | A film is projected in at least one (and many) halls (implied: it's not a film if it's never projected). |

# extracting association attributes

they are most commonly found mentioning an association between entities that require a condition or a detail that is an attribute (sometimes association attribute can be NOT a part of any association) (square what we suspect to be association attributes) an association only has attributes when its many to many

| **Relationship** | **Text Description Source**                                                                                 | **Relationship Attributes** |
| ---------------- | ----------------------------------------------------------------------------------------------------------- | --------------------------- |
| **Jouer**        | Des **cachets** sont reçus pour chaque acteur et chaque réalisateur pour chaque film dans lequel il a joué. | **Cachet**                  |
| **Projeter**     | Un film est projeté dans plusieurs salles à certaines **date et heure**.                                    | **DateProj**, **HeureProj** |
# How to read and understand corndinalities

lets assume we have the following:

1. entity A with cardinalities of (X and Y)
2. entity B with cardinalities of (W and Z)
3. association C

one instance of entity A is associated with at least X instances and at most Y instances of entity B through association C, and one instance of entity B is associated with at least W instances and at most Z instances of entity A through the same association C. 

![[image-37.png]]

in this example it reads

- one instance of student can be associated to one class
- one instance of class can be associated to 0 or N students

# Note

an association is defined by the primary key of the association meaning to full understand an association we need to think about it as a special entity that contains the primary keys of all the entities participated in that association