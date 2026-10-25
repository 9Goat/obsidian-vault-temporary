# Syntax

```Java
[access modifiers] [static] [final] datatype variableName [= initialValue];
```

- [[access modifiers]]
- [[Temporary/Java/class related/static]]
- [[final]]
- [[Datatypes]]
- [[how to name identifiers]]
- **initialValue** we have the option to provide our variable with an initial value.
# Example

```Java
public class VariableDisplay {
    public static void main(String[] args) {
        int score = 100;                 // An integer variable
        String playerName = "Hero";      // A string variable
        final boolean gameOver = false;  // A final boolean variable

        System.out.println("Player: " + playerName);
        System.out.println("Score: " + score);
        System.out.println("Game Over: " + gameOver);
    }
}
```