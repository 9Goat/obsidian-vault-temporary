
there are 3 types of points that we use in transitions which are the followings:

- junction points
- decisions points
- connection points

# Junction points

Junction pseudo-states are used to chain together multiple transitions. A single junction can have one or more incoming, and one or more outgoing, transitions; a guard can be applied to each transition.

- junction points **CANNOT** have internal activities, like events and triggers, they are only allowed to have conditions 

- for a state to over to the junction point it has to evaluate its condition to the junction point and validate **exactly one** condition from the junction point to an another state

![[image-398.png]]![[image-399.png]]

# Decision point

A choice pseudo-state is shown as a diamond with one transition arriving and two or more transitions leaving.used to represent different possible paths a transition can take.

Unlike a junction point, the guards located after the decision point are evaluated at the time it is reached. This allows the choice to be based on results obtained by crossing the segment before the decision point.

**In short**: its basically an if else statement, with the possibility of using *else* as a condition

![[image-400.png]]

# Connection points

**Connection points** are specific "gates" placed on the **outside border** of a composite state 

While standard transitions use the border to go to the default initial state, connection points are used when you need **specific, named entry or exit routes** for that super-state.

**Notation**

- **Entry Point:** Represented by a **small empty circle** on the border.
- **Exit Point:** Represented by a **small circle with a cross (X)** on the border.

![[image-410.png]]

