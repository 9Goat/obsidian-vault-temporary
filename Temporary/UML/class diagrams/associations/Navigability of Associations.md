# 1. Default Behavior (Bidirectional)

- **Rule:** By default, associations in UML are assumed to be **navigable in both directions** (bidirectional).
    - This means an instance of Class A can "see" and access instances of Class B, and an instance of Class B can "see" and access instances of Class A.
    - In code, this implies both classes would hold attributes referencing the other.

# 2. Unidirectional Navigability

- **Purpose:** An association may only require navigation in a **single direction** (unidirectional). This is used when a relationship is only meaningful or necessary from one viewpoint.
- **Notation:** Unidirectional navigation is represented by an **open-headed arrow** placed on the association line, pointing toward the class that is being accessed (the destination).

![[image-72.png]]

# Example

![[image-73.png]]![[image-74.png]]

