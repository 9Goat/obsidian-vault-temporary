
#  Introduction to strategy pattern

## Definition

**Strategy** is a behavioral design pattern that lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.This allows the specific behavior to change without needing to change the code that uses it.

## Benefits

- **Dynamic Change:** It allows an object to change its behavior **while the program is running**.
- **Isolation:** it keeps different behaviors separate so they don't clutter the main logic.
- **Better Maintenance:** It avoids the "traps" of inheritance, where adding a new feature to a parent class might accidentally give a weird behavior to a child class that shouldn't have it (like a plastic toy duck suddenly being able to fly).

## When to use

- Use the Strategy pattern when you want to use different variants of an algorithm within an object and be able to switch from one algorithm to another during runtime.
- Use the Strategy when you have a lot of similar classes that only differ in the way they execute some behavior.
- Use the pattern when your class has a massive conditional statement that switches between different variants of the same algorithm.

# How to implement strategy patterns

## The problem

lets say that we are working on a payment service where the client can pay with credit/bank/paypal ,,,etc so we come up with this solution:

```java
class PaymentService{
    public void processPayment(String paymentMethod) {
        
        if (paymentMethod.equals("CreditCard")) {
            System.out.println("Processing credit card payment of $" + cost);
            System.out.println("Client: " + client.name + ", Balance: $" + client.balance);
            client.balance -= cost;
        } else if (paymentMethod.equals("PayPal")) {
            System.out.println("Processing PayPal payment of $" + cost);
            System.out.println("Client: " + client.name + ", Balance: $" + client.balance);
            client.balance -= cost;
        } else if (paymentMethod.equals("BankTransfer")) {
            System.out.println("Processing bank transfer payment of $" + cost);
            System.out.println("Client: " + client.name + ", Balance: $" + client.balance);
            client.balance -= cost;
        }

        //The problem is that if we want to add a new payment method we have to modify the if statement
        //This violates the Open/Closed Principle
    }
}
```

- but when we want to change of add a new payment method we have to change the code directly by adding/removing/changing an if statement which violates the **SOLID** principal 

# Basic solution

## Strategy interface

instead of having all of the functionalities hardcoded in a single class, instead we should create an interface that contains those methods so we know exactly how our payment process will function

the class name will be **PaymentStrategy** since it holds all the methods for the implement of those strategies

```java
interface PaymentStrategy {
    void processPayment(double cost, Client client);
}
```

## implementation strategies

after defining the methods that we will be working with inside the strategy interface, we can then implement them differently with different methods

```java
class CreditCardPayment implements PaymentStrategy {
    @Override
    public void processPayment(double cost, Client client) {
        System.out.println("Processing credit card payment of $" + cost);
        System.out.println("Client: " + client.name + ", Balance: $" + client.balance);
        client.balance -= cost;
    }
}

class PayPalPayment implements PaymentStrategy {
    @Override
    public void processPayment(double cost, Client client) {
        System.out.println("Processing PayPal payment of $" + cost);
        System.out.println("Client: " + client.name + ", Balance: $" + client.balance);
        client.balance -= cost;
    }
}

class BankTransferPayment implements PaymentStrategy {
    @Override
    public void processPayment(double cost, Client client) {
        System.out.println("Processing bank transfer payment of $" + cost);
        System.out.println("Client: " + client.name + ", Balance: $" + client.balance);
        client.balance -= cost;
    }
}
```

## Context class

we call the class that is responsible for using the strategy interface as *context class*, the context will be linked with the interface via composition

```java
class PaymentService {
    double cost;
    Client client;
    PaymentStrategy paymentStrategy;

    PaymentService(double cost, Client client, PaymentStrategy paymentStrategy) {
        this.cost = cost;
        this.client = client;
        this.paymentStrategy = paymentStrategy;
    }
    
    public void setStrategy(PaymentStrategy paymentStrategy){
	    this.paymentStrategy = paymentStrategy;
    }

    public void processPayment() {
        paymentStrategy.processPayment(cost, client);
    }
}
```

## Client/User (Optional)

we need a client or use to decide which strategy to use and execute it via the context class

```java
public class WithStrategy {
    public static void main(String[] args) {
        Client client = new Client(1000, "John Doe");
        PaymentService paymentService = new PaymentService(200, client, new CreditCardPayment());

        paymentService.processPayment();

        paymentService = new PaymentService(200, client, new PayPalPayment());
        paymentService.processPayment();

        paymentService = new PaymentService(200, client, new BankTransferPayment());
        paymentService.processPayment();
    }
}
```

![[image-350.png]]

