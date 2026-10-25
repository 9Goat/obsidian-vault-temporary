 there are 4 main types of events in a transation which are the followings:
- Call
- Signal
- change
- after or when 

# Signal

A **Signal Event** is like a message sent from one object to another. In UML, it is defined as an **asynchronous stimulus**.

"Asynchronous" is a fancy way of saying that the object sending the signal doesn't stop and wait for a response; it just sends the "shout" and moves on.

there are 2 steps of making a signal in state diagram which are the followings:

- create/declare the signal
- use the signal as the event of the transition 

## Creating the signal 

a signal is an event so create a rectangle and put the name of the signal inside it alongside the `<<singal>>` sign

![[image-391.png]]

## Using the signal 

just use the signal name as the name of the event causing the transition

![[image-392.png]]


# Event calls

A call event represents the dispatch of an operation from one object to another..Because it is a specific operation, it can include **parameters**, which are extra pieces of information needed to complete the task

![[image-393.png]]
![[image-394.png]]


# Change

A **Change Event** is a trigger that happens when a specific **boolean condition** (a statement that is either true or false) becomes true.

In a diagram, this is written as `when(condition)`. The most important thing to know is that this condition is **evaluated continuously**. The system keeps checking it over and over until the condition finally becomes true, which then immediately triggers the state change.

## 2 types of conditions

- **Guard Condition:** Checked **only once** when a specific event happens. If it is false at that exact moment, the transition doesn't happen, and the system stops checking it.
- **Change Event:** Checked **constantly**. It waits patiently until the condition is met.

![[image-395.png]]

# after or when

A **Temporal Event** is a trigger that happens simply because **time has passed**. You don't need an outside person or another object to do anything; the system's clock handles it.

There are two ways to write these conditions:

1. **Relative Time (****after****):** This counts how much time has passed **since the object entered the current state**. It is like a countdown timer.
    - _Example:_ `after(5 seconds)`.
2. **Absolute Time (****when****):** This refers to a **specific, exact date or time**.
    - _Example:_ `when(date = January 1, 2025)`.

![[image-396.png]]
![[image-397.png]]





