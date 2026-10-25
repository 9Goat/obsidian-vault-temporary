
method overloading is a feature in java that allows use to have more than one method with the same name as long as we have:

- **different parameters**: they parameters can be different in terms of the number of the parameters or in terms of the datatype of the parameters.

### Example

```Java
public class methodOverloading {
    public static void main(String[] args){
        testing obj = new testing();
        obj.display(5);
        obj.display("Hello");
        obj.display(10, "World");
    }
    }
    
class testing{
    public void display(int a){
        System.out.println("Integer: " + a);
    }

    public void display(String b){
        System.out.println("String: " + b);
    }

    public void display(int a, String b){
        System.out.println("Integer: " + a + ", String: " + b);
    }
}
```

## Note 

- it is **NOT** possible to have a method outside a class
- method overloading also applies to [[Constructors]]
