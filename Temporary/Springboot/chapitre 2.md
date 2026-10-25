# MVC Layered Architecture

- **Presentation Layer (Controllers)**: Handles HTTP requests from users, calls services, and sends back responses like JSON.
- **Service Layer (Business Logic)**: Contains your app's rules, like validating data or combining operations. It sits between controllers and data access, keeping business logic separate.
- **Persistence Layer (Repositories)**: Talks to the database with CRUD(**CREATE,READ,UPDATE,DELETE**) operations and custom queries. It hides SQL details, returning Java objects instead.
- **Model Layer (Entities)**: Java classes that map to database tables, with validations.

|Layer|Role|Spring Annotation|
|---|---|---|
|**Presentation**|Receives HTTP requests from the user|`@RestController`|
|**Service**|Contains the business logic & validations|`@Service`|
|**Repository**|Talks to the database|`@Repository`|
|**Model**|Represents your data (Java ↔ DB table)|`@Entity`|

**The flow works like this:**

```
User → Controller → Service → Repository → Database
                                              ↓
User ← Controller ← Service ← Repository ← Database
```

## Benefits

- **Separation of Concerns:** Each layer has exactly one responsibility, making the code easier to maintain and change without affecting other layers.
- **Testability:** You can test a Service independently without needing the Controller.

# JPA

we use **JPA (Java Persistence API)** to turn a simple Java class into a database table.

JPA is a type of **ORM — Object-Relational Mapping**. It's just a fancy way of saying _"a tool that maps Objects (Java) to Relations (SQL tables)"_.

## How jpa turns objects to tables

```Java
@Entity                         // This class = a database table
@Table(name = "produit")        // The table is named "produit"
public class Produit {

    @Id                         // This field = the primary key
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Auto-increment
    private Long id;

    @Column(name = "nom")       // This field = a column called "nom"
    private String nomProduit;

    @Column(name = "prix")
    private Double prixProduit;
}


JPA reads these annotations and automatically knows:
- Which **table** to query
- Which **column** maps to which **field**
- How to **generate IDs**

Here's a simple visual of the mapping:

Java Class          →      Database Table
──────────────────────────────────────────
Produit             →      produit
id (Long)           →      id (BIGINT)
nomProduit (String) →      nom (VARCHAR)
prixProduit(Double) →      prix (DECIMAL)
```

| Annotation                                          | Purpose                          |
| --------------------------------------------------- | -------------------------------- |
| `@Entity`                                           | Marks class as database-mappable |
| `@Table(name="produit")`                            | Custom table name                |
| `@Id`                                               | Primary key field                |
| `@GeneratedValue(strategy=GenerationType.IDENTITY)` | Auto-generate ID                 |
| `@Column(name="nom_produit", nullable=false)`       | Maps field to column             |

# The Persistence Layer (Spring Data JPA Repositories)

Think of a Repository like a **remote control for your database**. Instead of writing SQL queries yourself, you just call methods like:

- `save()` → INSERT into the database
- `findById()` → SELECT by ID
- `findAll()` → SELECT everything
- `delete()` → DELETE from the database

## How to create a repository

```Java
@Repository
public interface ProduitRepository extends JpaRepository<Produit, Long> {
    // That's it! Spring auto-creates:
    // - save(), findAll(), findById(), deleteById(), count()
}
```

That's it. Spring Boot sees this interface and **automatically creates a full working implementation** behind the scenes. You get all basic CRUD operations for free.

The `<Produit, Long>` part tells Spring:

- **Produit** → which entity this repository manages
- **Long** → the type of the primary key (the `id` field)

## Repository methods

Just by extending `JpaRepository`, you instantly have access to:

|Method|What it does|
|---|---|
|`save(entity)`|Insert or update|
|`findById(id)`|Find one by ID|
|`findAll()`|Get all records|
|`deleteById(id)`|Delete by ID|
|`count()`|Count all records|
|`existsById(id)`|Check if a record exists|

##  Custom repositories

Sometimes you need more than just "find by ID". For example, what if you want to **find all products under a certain price**? You can add custom methods using Spring's **method naming convention**:

```Java
@Repository
public interface ProduitRepository extends JpaRepository<Produit, Long> {

    // Spring reads the method name and generates the SQL automatically!
    List<Produit> findByNomProduit(String nom);
    List<Produit> findByPrixProduitLessThan(Double prix);
    List<Produit> findByNomProduitContaining(String keyword);
}
```

#  Service layer

**Service Layer** is where your business logic lives. It's an interface + implementation that sits between Controllers and Repositories, adding validation, rules, and orchestration.

**Repository = Data access only.** Service = **Business rules + validation + multiple operations**

the service layers gets divided into 2 sections which are:

- the interface defines whats the service can do
- implementation defines the business logic and data validation (how its going to execute).

## Interface

defines _WHAT_ the service can do (the contract):

```java
public interface ProduitService {
    Produit saveProduit(Produit produit);
    Produit getProduitById(Long id);
    List<Produit> getAllProduits();
    void deleteProduit(Long id);
}
```

## implementation

defines _HOW_ it does it (the actual logic):

```java
@Service
public class ProduitServiceImpl implements ProduitService {

    @Autowired
    private ProduitRepository produitRepository;

    @Override
    public Produit saveProduit(Produit produit) {
        // Business rule: name cannot be empty
        if (produit.getNomProduit() == null || produit.getNomProduit().isBlank()) {
            throw new IllegalArgumentException("Product name is required!");
        }
        // Business rule: price must be positive
        if (produit.getPrixProduit() <= 0) {
            throw new IllegalArgumentException("Price must be greater than 0!");
        }
        // Only if valid, save to database
        return produitRepository.save(produit);
    }

    @Override
    public Produit getProduitById(Long id) {
        return produitRepository.findById(id)
            .orElseThrow(() -> new RuntimeException("Product not found!"));
    }
}
```

# Entities

An Entity is simply a **Java class that represents a table in your database**. Every instance of that class represents **one row** in that table.

## Class annotations

```java
@Entity
@Table(name = "produit")
```

|Annotation|What it does|
|---|---|
|`@Entity`|Tells JPA this class maps to a database table|
|`@Table(name = "produit")`|Specifies the exact table name in the database|

If you skip `@Table`, JPA will use the class name as the table name by default.

### Lombok

Without Lombok, every entity needs dozens of lines of repetitive code:

java

```java
// ❌ Without Lombok — so much repetitive code!
public String getNomProduit() { return nomProduit; }
public void setNomProduit(String nom) { this.nomProduit = nom; }
public Double getPrixProduit() { return prixProduit; }
public void setPrixProduit(Double prix) { this.prixProduit = prix; }
// ... and so on for every field
```

With Lombok annotations, one line replaces all of that:

```java
// ✅ With Lombok — clean and simple!
@Data           // Generates ALL getters, setters, toString, equals, hashCode
@NoArgsConstructor  // Generates: public Produit() {}
@AllArgsConstructor // Generates: public Produit(Long id, String nom, Double prix...)
@Builder            // Enables the builder pattern
```

### Builder

`@Builder` gives you a clean way to create objects with many fields:

```java
// ❌ Without Builder — hard to read, easy to mix up parameter order
Produit p = new Produit(null, "Laptop", 1200.0, 50);

// ✅ With Builder — clear, readable, flexible
Produit p = Produit.builder()
    .nomProduit("Laptop")
    .prixProduit(1200.0)
    .quantiteStock(50)
    .build();
```

With the builder you can clearly see **which value goes to which field**, and you can skip optional fields easily.

## Column annotations

```java
@Column(name = "nom", length = 100, nullable = false)
private String nomProduit;
```

|Property|What it does|
|---|---|
|`name = "nom"`|The column name in the database|
|`length = 100`|Maximum character length (for Strings)|
|`nullable = false`|This column cannot be NULL in the database|

### Validation annotations

These annotations **reject bad data before it even reaches the database**:

```java
@NotBlank(message = "Product name is required")
private String nomProduit;

@Positive(message = "Price must be greater than 0")
private Double prixProduit;

@Min(value = 0, message = "Stock cannot be negative")
private Integer quantiteStock;
```

|Annotation|What it validates|
|---|---|
|`@NotBlank`|String is not null and not empty|
|`@NotNull`|Value is not null|
|`@Positive`|Number is greater than 0|
|`@Min(value)`|Number is greater than or equal to value|
|`@Max(value)`|Number is less than or equal to value|

## Example 

```java
@Entity                         // 1. This class is a database table
@Table(name = "produit")        // 2. The table name in the database
@Data                           // 3. Lombok - generates getters/setters
@NoArgsConstructor              // 4. Lombok - generates empty constructor
@AllArgsConstructor             // 5. Lombok - generates full constructor
@Builder                        // 6. Lombok - enables builder pattern
public class Produit {

    @Id                                                    // Primary key
    @GeneratedValue(strategy = GenerationType.IDENTITY)   // Auto-increment
    private Long idProduit;

    @NotBlank(message = "Product name is required")       // Validation
    @Column(name = "nom", length = 100, nullable = false) // Column config
    private String nomProduit;

    @Positive(message = "Price must be greater than 0")   // Validation
    @Column(name = "prix", nullable = false)
    private Double prixProduit;

    @Min(value = 0, message = "Stock cannot be negative") // Validation
    @Column(name = "stock")
    private Integer quantiteStock;
}
```

# Database  configuration

the `application.properties` File

This file lives at:

```
src/main/resources/application.properties
```

## database connection

### database url

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/produit_db
```

This is the **address of your database**. Let's read it like a sentence:

```
jdbc:mysql://localhost:3306/produit_db
│    │       │         │    │
│    │       │         │    └── Database name
│    │       │         └─────── Port (MySQL default)
│    │       └───────────────── Host (your machine)
│    └───────────────────────── Database type
└────────────────────────────── Java database protocol
```

### account and password

```properties
spring.datasource.username=root
spring.datasource.password=root
```

Your MySQL **login credentials**. In production you would never use `root` — you'd create a dedicated user with limited permissions.

###  database  driver

```properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

Tells Spring which **MySQL driver** to use to communicate with the database

## Hibernate settings


```properties
spring.jpa.hibernate.ddl-auto=update
```

This controls **what Hibernate does to your database tables** when the application starts. This is the setting students get wrong the most:

|Value|What it does|When to use|
|---|---|---|
|`create`|Drops and recreates tables every startup|❌ Dangerous — deletes all data|
|`create-drop`|Creates tables on startup, drops on shutdown|Only for quick tests|
|`update`|Updates tables to match your entities|✅ Development|
|`validate`|Checks tables match entities, fails if not|✅ Production|
|`none`|Does nothing to the database|When you manage DB yourself|
### debugging

```properties
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

With these enabled, every SQL query Hibernate generates gets printed in your console:

```sql
INSERT INTO produit (nom, prix, stock)
VALUES ('Laptop', 1200.0, 50)
```

This is extremely useful for **debugging** — you can see exactly what queries are being executed behind the scenes.

### sql  syntax

```properties
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
```

Different databases (MySQL, PostgreSQL, Oracle) have slightly different SQL syntax. The **dialect** tells Hibernate which flavor of SQL to generate.

Think of it like telling someone:

> _"When you talk to this database, speak MySQL, not PostgreSQL."_

#  Unit testing

A unit test is a piece of code that **automatically verifies that your code behaves correctly**. You write it once and run it anytime to make sure nothing is broken.

## Setting Up a Test Class

In Spring Boot, a test class looks like this:


```java
@SpringBootTest                 // Load the full Spring application context
@Transactional                  // Roll back database changes after each test
class ProduitServiceTest {

    @Autowired
    private ProduitService produitService;

    @Autowired
    private ProduitRepository produitRepository;
}
```

| Annotation        | What it does                                      |
| ----------------- | ------------------------------------------------- |
| `@SpringBootTest` | Starts the full Spring app for testing            |
| `@Transactional`  | Rolls back all database changes after each test   |
| `@Autowired`      | Injects the real service/repository into the test |

## 3 types of tests

- **Happy path**: Normal cases (save valid product)
- **Error cases**: Invalid data (null name, negative price)
- **Edge cases**: Empty lists, boundary values

### Type 1: Happy Path Tests ✅

Testing that things work correctly under **normal conditions**:

```java
@Test
void testSaveProduit_Success() {
    // 1. ARRANGE — prepare your data
    Produit produit = Produit.builder()
        .nomProduit("Laptop")
        .prixProduit(1200.0)
        .quantiteStock(10)
        .build();

    // 2. ACT — call the method you're testing
    Produit saved = produitService.saveProduit(produit);

    // 3. ASSERT — verify the result is correct
    assertThat(saved).isNotNull();
    assertThat(saved.getIdProduit()).isNotNull();
    assertThat(saved.getNomProduit()).isEqualTo("Laptop");
}
```

---

### Type 2: Error/Edge Case Tests ❌

Testing that your code **handles bad data correctly**:

```java
@Test
void testSaveProduit_EmptyName_ShouldFail() {
    // Arrange — bad data on purpose
    Produit produit = Produit.builder()
        .nomProduit("")         // Empty name — should be rejected
        .prixProduit(1200.0)
        .build();

    // Assert — verify that an exception is thrown
    assertThatThrownBy(() -> produitService.saveProduit(produit))
        .isInstanceOf(IllegalArgumentException.class)
        .hasMessageContaining("name is required");
}

@Test
void testSaveProduit_NegativePrice_ShouldFail() {
    Produit produit = Produit.builder()
        .nomProduit("Laptop")
        .prixProduit(-100.0)    // Negative price — should be rejected
        .build();

    assertThatThrownBy(() -> produitService.saveProduit(produit))
        .isInstanceOf(IllegalArgumentException.class);
}
```

---

### Type 3: Boundary/Limit Tests 🔲

Testing the **exact edges** of your rules:

```java
@Test
void testSaveProduit_ZeroPrice_ShouldFail() {
    // Zero is the exact boundary — is it allowed or not?
    Produit produit = Produit.builder()
        .nomProduit("Laptop")
        .prixProduit(0.0)       // Exactly at the boundary
        .build();

    assertThatThrownBy(() -> produitService.saveProduit(produit))
        .isInstanceOf(IllegalArgumentException.class);
}

@Test
void testSaveProduit_MinimumValidPrice_ShouldSucceed() {
    Produit produit = Produit.builder()
        .nomProduit("Laptop")
        .prixProduit(0.01)      // Just above the boundary — should work
        .build();

    Produit saved = produitService.saveProduit(produit);
    assertThat(saved).isNotNull();
}
```

# public annotations

##  Autowired

Spring creates **one single shared instance** of each bean and reuses it everywhere. This is called a **Singleton** — one instance for the entire application.

```
Spring creates:
──────────────────────────────────────
1 instance of ProduitRepository
1 instance of ProduitServiceImpl  → gets the SAME repository instance
1 instance of ProduitController   → gets the SAME service instance
```

### How Does Spring Know What to Inject?

Spring keeps a list of all available objects (called **beans**). A bean is any class annotated with:

- `@Service` → Service classes
- `@Repository` → Repository classes
- `@Component` → General classes
- `@RestController` → Controller classes

When Spring sees `@Autowired`, it looks through its list of beans, finds the matching type, and injects it.

```
Spring's Bean List:
─────────────────────────────
✅ ProduitRepository  (bean)
✅ ProduitServiceImpl (bean)
✅ ProduitController  (bean)

@Autowired ProduitRepository
→ Spring finds it in the list ✅
→ Spring injects it automatically ✅
```

With `@Transactional`, Spring says:

> _"All steps inside this method are ONE single unit. Either ALL of them succeed and get saved, or if ANYTHING fails, I will undo everything back to how it was before."_

This "undo" is called a **Rollback**.

`@Transactional(readOnly = true)`
When you're only **reading** data (not changing anything), you can use:

java

```java
@Transactional(readOnly = true)
public List<Produit> getAllProduits() {
    return produitRepository.findAll();
}
```

This tells Spring:

> _"I promise I won't modify anything here — just reading."_

This makes the operation **faster** because Spring skips some safety checks it only needs for write operations.


