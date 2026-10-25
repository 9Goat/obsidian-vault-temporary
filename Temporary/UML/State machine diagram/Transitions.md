# 1. What are Transitions?

A **Transition** is a relationship between two states indicating that an object in the first state will enter the second state when a specific event occurs and certain conditions are met.

- **Visual:** Represented as a solid arrow pointing from the **Source State** to the **Target State**.

---

# 2. What is a Transition Made Of?

In UML, a transition has a very specific "syntax" or signature. It is usually written along the arrow in this format: **`Trigger [Guard] / Effect`**

- **Trigger (The Event):** The "cause" that kicks off the transition (e.g., `Button Pressed`, `Timer Expired`).
- **Guard (The Condition):** A Boolean (True/False) check. The transition only happens if this is true (e.g., `[temperature > 100]`). It is always written in square brackets.
- **Effect (The Action):**  instantaneous and atomic, therefore uninterruptible. behavior that happens _during_ the transition (e.g., `/ play sound`). An action can include operation calls, the creation or destruction of an object, ....

![[image-321.png]]
![[image-390.png]]

---

# 3. Types of Transitions

There are four main types you’ll encounter:

## A. External Transition

The most common type. It exits the current state and enters a **different** state.
- **Result:** Triggers the `exit` action of State A and the `entry` action of State B.

![[image-323.png]]

## B. Self-Transition

An arrow that leaves a state and loops back to point at the **same** state.

- **Result:** It actually **exits and re-enters** the state. This means the `exit` actions run, and then the `entry` actions run again.

![[image-322.png]]

## D. Completion (Triggerless) Transition

An arrow with no text (no trigger).

- **Result:** The transition happens automatically as soon as the state's `do` activity finishes.
	- ![[image-324.png]]
## Forks and joins

A **fork in an activity diagram** is a control node that splits the flow of control into multiple, concurrent flows. It allows for parallel execution of activities, where different sub-processes or tasks can be executed simultaneously.  a join is their ending point where all of those forked transitions meet to conclude in an another state

![[image-411.png]]
