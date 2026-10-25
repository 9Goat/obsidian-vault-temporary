# How to determine actors

## How to determine generalisation actor

when we compare an actor to an another by using keywords like these:

- meme functionality que `<<actor>>`

# How to determine use cases

## How to determine include use cases

when we see those words then there is a high chance that is refers to include:

- doit
- il fault
- toujours
- pendant que
- via

when we determine that there is an authentication use case, we could make it an include to ALL existing use cases that the user can interact with 

## How to determine extend use cases

when we see those words then there is a high chance that is refers to extend:

- peut
- si
- lorsque
- dans la ca ou

# How to read the text

when we suspect that a word is an actor we add it to a list of the left where we underline the secondary actors and double underline the generalisation (specific actor) actor

otherwise if we suspect that a sentence or a group of sentences describe a use case, we add it to a list on the right. Where we connect those use cases by writing the order of the actor behind  it and underline the included use case and double underline the extended use case. and we put in square the generalization (specific use case) use case

# Description

## identifier

only focus on the first 3 details of the indetifier:

- nom du case 
- objective
- actors

## Pre/post condition 

we write it in a list like this 

- le client valide le command
- le commande avoir un statut "en cours"

## enchainement

in the alternatives and error scenarios we also write in list this way:

- A1 or E1 en (3 du scenario nominal): Si {{condition}} ,le {{acteur}} doit ,,,,,

the difference between the 2 is that in the alternative the actors reaches his goal while in the error the actors doesnt