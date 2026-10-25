
# 1. What makes a State?

Unlike the start and end points, a state represents a period of time where the object is **stable**.

- **Visual:** It is represented by a rectangle with rounded corners.
- **Examples:** If you are modeling a "Light Bulb," the states are **On** and **Off**. If you are modeling an "Order," the states might be **Pending**, **Shipped**, and **Delivered**.

![[image-317.png]]

# 2. internal states

Internal states refer to the set of actions and behaviors defined within a state, without changing states

A state can be more than just a name; it can contain internal behaviors divided into three compartments:

- **Entry:** Actions performed immediately when entering the state (e.g., `entry / turn on light`).
	- ![[image-320.png]]
- **Do:** Ongoing **activity** (meaning its active during the entire lifetime of the state) performed while the object is in that state (e.g., `do / blink light`).
	- ![[image-318.png]]
- **Exit:** Actions performed just before leaving the state (e.g., `exit / log timestamp`).
- **Internal transitions**: these are just events and conditions that happen inside the state without changing the state itself
	- ![[image-401.png]]

# Composite state

if a state diagram become too complex, its better to include some states inside others to show connections

## Benefits

- hierarchy structure of states 
- makes complex structures easier to understand

## Example of transitioning from normal to composite

![[image-402.png]]
![[image-403.png]]
![[image-404.png]]

## Reference

to reference a composite state inside another diagram, we dont have to rewrite the entire state again, we can just use this notation (basically looks like glasses o-o) to indicate that the definition of this diagram in written in an another diagram

![[image-405.png]]


## Transition between composite states

- **Targeting the Boundary (Entering):** If a transition arrow points directly to the **outside border** of a composite state, it is the same as pointing to the **initial sub-state** inside.
- **Originating from the Boundary (Leaving):** If a transition arrow starts from the **outside border** of a composite state, that transition applies to **every sub-state inside**.

![[image-406.png]]

# History states

Normally, when an object enters a composite state, it starts over from the very beginning (the initial sub-state). However, if an interruption happens (like a power cut), you might want the object to **remember where it was** and pick up exactly where it left off. This is what the historical state does.

there are 2 types of history states which are the followings

1. **Shallow History (noted as "H" in a circle):** This only remembers the last active sub-state at the **top level** of the container. It does not remember the details if there are even smaller states nested inside those sub-states.
2. **Deep history (noted as "H*" in a circle)**: This is a "deep memory." It remembers the last active state at **every level of nesting**, no matter how deep it goes. It restores the entire configuration of the object.

- **Note** when we first enter a state and we have no memory, then an interuption happens we use the arrow of the history state to know which substate we are supposed to start with

![[image-407.png]]
![[image-408.png]]
![[image-409.png]]

# Concurrent states

Concurrent states allow an object to be in **more than one state at the exact same time**. This happens when you divide a composite state into different **regions** using a **dotted line**.

**How it works:**

- **Parallel Action:** Instead of doing tasks one after another, the object performs tasks in each region **simultaneously**.
- **Independent Flows:** Each region represents its own "flow of execution".
- **The Completion Rule:** You can only exit the main super-state once **every single sub-automaton** inside has reached its own final state.



