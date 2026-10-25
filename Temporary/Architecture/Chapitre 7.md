
we will explore three specific structural object patterns:

1. **Decorator:** Used to **dynamically attach additional responsibilities** to an object, providing a flexible alternative to subclassing.
2. **Adapter:** Used to **convert the interface** of a class into another interface that a client expects, allowing incompatible classes to work together.
3. **Proxy:** Used to provide an **intermediary** or placeholder for another object to control access to it.
# Introduction

While **Creational Patterns** focus on the processes used to instantiate objects, **Structural Patterns** are concerned with how classes and objects are **composed** to form larger, more complex structures. They provide ways to organize your code so that different parts of a system can work together efficiently and flexibly.

# Decorator pattern

Think of the Decorator pattern like **wrapping a gift**. You start with the gift itself (the **Component**). Then, you put it in a box (the first **Decorator**). Finally, you wrap that box in colored paper and add a ribbon (a second **Decorator**).

Even though you've added many "layers," it is still fundamentally a gift. you can add as many layers as you want

## Problem

lets say we have a simple notification service where we want to send notification with email, sms and whatsapp, the problem is that normally we can only choose one of the following options to execute in a single method, so what we do is create a class that combines all of them into a single method

```java
class EmailSmsAndWhatsAppNotification extends Notification {
    @Override
    public void send(String message) {
        super.send(message); // Sends Email
        System.out.println("Sending SMS: " + message);
        System.out.println("Sending WhatsApp Message: " + message);
    }
}
```

- the problem is that the larger our app becomes and the more notification types we add, the more complicated our classes will be

## interface component and their concrete components

lets say that we have different types of notifications that can range from:

- information
- alert
- warning

we want to have a class for each of them, to make that possible we need an interface component with the methods to override

**Interface**

```java
interface ComponentNotification {
    void send(String message);
}
```

**Implementation**

```java
class CoreAlertNotification implements ComponentNotification {
    @Override
    public void send(String message) {
        System.out.println("Sending Alert: " + message);
    }
}

class CoreWarningNotification implements ComponentNotification {
    @Override
    public void send(String message) {
        System.out.println("Sending Warning: " + message);
    }
}

class CoreInfoNotification implements ComponentNotification {
    @Override
    public void send(String message) {
        System.out.println("Sending Info: " + message);
    }
}
```

## Decorator Implementation

To implement the Decorator pattern, we need to create a Decorator class that implements the ComponentNotification interface. and below it we will have decorator implementation classes .

**Interface**

```java
abstract class NotificationDecorator implements ComponentNotification {
    protected ComponentNotification wrappedNotifier; 

    public NotificationDecorator(ComponentNotification notifier) {
        this.wrappedNotifier = notifier;
    }

    @Override
    public void send(String message) {
        wrappedNotifier.send(message); 
    }
}
```

- the decorator implements the component to override its method, aka just send the message with no special modification
- the decoator contains a composition relation with the component so that it uses it to send the message

**Implementation**

```java
class SmsDecorator extends NotificationDecorator {
    public SmsDecorator(ComponentNotification notifier) {
        super(notifier);
    }

    @Override
    public void send(String message) {
        super.send(message); 
        System.out.println("Sending SMS: " + message);
    }
}

class WhatsAppDecorator extends NotificationDecorator {
    public WhatsAppDecorator(ComponentNotification notifier) {
        super(notifier);
    }

    @Override
    public void send(String message) {
        super.send(message); // Run previous layers
        System.out.println("Sending WhatsApp Message: " + message); 
    }
}
```

- with `super.send(message)` we essentially execute 2 methods at once which are:
	- the original component method
	- our new extended whatsapp method
- to make that possible we have to pass the original component notification to the constructor with super

## user/client

```java
public class WithDecorator {
    public static void main(String[] args) {
        ComponentNotification notifier = new CoreAlertNotification();

        notifier = new SmsDecorator(notifier);

        notifier = new WhatsAppDecorator(notifier);

        System.out.println("--- Triggering Stacked Notification ---");
        notifier.send("System maintenance scheduled for 2 AM.");
    }
}
```

- to made more notifications we simple have to create a new notification and give its constructor parameter our previous notification

![[image-355.png]]

![[image-356.png]]

![[image-357.png]]

# Adapter design pattern

this pattern allows two classes to work together that normally couldn't because their method names or parameters don't match.

there are two common ways to build an adapter:

1. **Adapter by Inheritance (Class Adapter):** The adapter class inherits from the class it is adapting (`ImplAdaptee`) and also implements the standard interface.
2. **Adapter by Composition (Object Adapter):** The adapter class implements the standard interface but holds a **private instance** of the class it is adapting. This is generally considered more flexible.

## The problem

lets say that we are a music company that accepts mp3 files and play it as music, then we decided to add support to play music for mp4 files, the problem is that we cant modify the code of the mp4 class (since its closed source or out or fear we break the code), aka we cant implement the play interface since it is not compatible with the mp3 file

```java
public class WithoutAdapter {
    public static void main(String[] args) {
        Mp4Player1 mp4Player = new Mp4Player1();
        MP4File mp4File = new MP4File("video.mp4", 1920, 1080);
        mp4Player.PlayMp4(mp4File);

        MediaPlayer1 mp3Player = new Mp3Player1();
        MP3File mp3File = new MP3File("song.mp3");
        mp3Player.play(mp3File);
}
}

class MP3File {
    private String fileName;

    public MP3File(String fileName) {
        this.fileName = fileName;
    }

    public String getFileName() {
        return fileName;
    }
}

class MP4File {
    private String fileName;
    private int width;
    private int height;

    public MP4File(String fileName, int width, int height) {
        this.fileName = fileName;
        this.width = width;
        this.height = height;
    }

    public String getFileName() {
        return fileName;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }
}

class Mp4Player1 {
    public void PlayMp4(MP4File mp4File) { 
        System.out.println("MP4 playing: " + mp4File.getFileName()+" with dimensions "+mp4File.getWidth()+"x"+mp4File.getHeight()); 
    }
}


interface MediaPlayer1 {
    void play(MP3File mp3File);
}

class Mp3Player1 implements MediaPlayer1 {
    public void play(MP3File mp3File) { 
        System.out.println("Playing native MP3: " + mp3File.getFileName()); 
    }
}

```

## standard components

before the mp4 feature we had the following components:

- a media interfaces that contains the play method
- mp3 class that implements the media interface to play music
- and an mp3 file class

```java
interface MediaPlayer1 {
    void play(MP3File mp3File);
}

class Mp3Player1 implements MediaPlayer1 {
    public void play(MP3File mp3File) { 
        System.out.println("Playing native MP3: " + mp3File.getFileName()); 
    }
}

class MP3File {
    private String fileName;

    public MP3File(String fileName) {
        this.fileName = fileName;
    }

    public String getFileName() {
        return fileName;
    }
}
```

## Adapter components

the adapter introduces the following components:

- an mp4 file
- mp4 player class that only works with mp4 files
- an adapter class that does the following:
	- contains composition of the mp4 player to execute its method(or instead of composition we can just inheritance with extend)
	- a convert method that transforms the mp3 file into mp4
	-  the overriden method that calls the transform method and runs the mp4 player method

```java
class MP4File {
    private String fileName;
    private int width;
    private int height;

    public MP4File(String fileName, int width, int height) {
        this.fileName = fileName;
        this.width = width;
        this.height = height;
    }

    public String getFileName() {
        return fileName;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }
}



class Mp4Player {
    public void PlayMp4(MP4File mp4File) { 
        System.out.println("MP4 playing: " + mp4File.getFileName()+" with dimensions "+mp4File.getWidth()+"x"+mp4File.getHeight()); 
    }
}

class adapterMp4Player implements MediaPlayer {
    private Mp4Player mp4Player;
    private int width;
    private int height;

    public adapterMp4Player(int width, int height) {
        this.mp4Player = new Mp4Player();
        this.height = height;
        this.width = width;
    }

    public void play(MP3File mp3File) {
        MP4File mp4File = transformToMP4(mp3File);
        mp4Player.PlayMp4(mp4File);
    }

    public MP4File transformToMP4(MP3File mp3File) {
        return new MP4File(mp3File.getFileName(), this.width, this.height);
    }
}
```


## User/client

we will create an mp3 file and pass it to both the standard mp3 player class and the adapter class to transform and play it in mp4

```java
public class WithAdapter {
    public static void main(String[] args) {
        MediaPlayer mp3Player = new Mp3Player();
        MP3File mp3File = new MP3File("song.mp3");
        mp3Player.play(mp3File);

        MediaPlayer mp4Player = new adapterMp4Player(1920, 1080);
        mp4Player.play(mp3File);
    }
}
```

- in case also have to add support to more formats like VLC we can just create a new adapter and transform from mp3 to adapter

![[image-359.png]]
![[image-360.png]]
![[image-361.png]]


# Proxy

The primary goal of the Proxy pattern is to provide an **intermediary** between the client and an object specifically to **control access** to that object. This allows you to isolate the behavior related to _how_ an object is accessed from the actual logic of the object itself.

the main use cases of proxy is the following:

**Security:** To verify access conditions or user permissions before triggering a sensitive operation.
**Logging requests (logging proxy).** This is when you want to keep a history of requests to the service object.

## Problem

in this application we have the following

- a user class that will access the database
- database interface that provides the common methods for the database
- postgress database class as our database implementation

```java
class User {
    private String username;
    private String role;
    private boolean isAuthenticated = false;

    public User(String username, String role) {
        this.username = username;
        this.role = role;
    }

    public boolean isAuthenticated() {
        return isAuthenticated;
    }

    public void setAuthenticated(boolean authenticated) {
        isAuthenticated = authenticated;
    }

    public String getUsername() {
        return username;
    }

    public String getRole() {
        return role;
    }
}

interface Database {
    public ArrayList<String> getDatabases();
    public void createDatabase(String name);
    public void deleteDatabase(String name);
    public void query(String sql);
    public void connect(User user);
    public void disconnect(User user);
}

class PostgreSQLDatabase implements Database {
    private ArrayList<String> databases = new ArrayList<>();

    public ArrayList<String> getDatabases() {
        return databases;
    }

    public void deleteDatabase(String name) {
        databases.remove(name);
        System.out.println("Database deleted: " + name);
    }

    public void createDatabase(String name) {
        databases.add(name);
        System.out.println("Database created: " + name);
    }

    public void query(String sql) {
        System.out.println("Executing SQL: " + sql);
    }

    public void connect(User user) {
        System.out.println("Connecting to PostgreSQL database as " + user.getUsername() + "...");
        user.setAuthenticated(true);
    }

    public void disconnect(User user) {
        System.out.println("Disconnecting from PostgreSQL database as " + user.getUsername() + "...");
        user.setAuthenticated(false);
    }
}
```

- the problem with this current code is that there is not verification of the existence of the database of the user role/authentification when accessing the database
- the problem of hardcoding the verification is that we will also have to provide the same verification for the other implementations like the MySQL database or the MongoDB databases

## Proxy class

the solution to this is to create a proxy class that contains the verification methods and directly call the implementation class

```java
class Proxy implements Database {
    private PostgreSQLDatabase realDatabase;

    public Proxy() {
        this.realDatabase = new PostgreSQLDatabase();
    }

    //verification methods

    public boolean hasAccess(User user) {
        return user.getRole().equals("admin");
    }

    public boolean isAuthenticated(User user) {
        return user.isAuthenticated();
    }

    public boolean DatabaseExists(User user, String name) {
        if (!isAuthenticated(user)) {
            System.out.println("Access denied: User is not authenticated.");
            return false;
        }
        return realDatabase.getDatabases(user).contains(name);
    }

    //Database methods

    public ArrayList<String> getDatabases(User user) {
        if (!isAuthenticated(user)) {
            System.out.println("Access denied: User is not authenticated.");
            return new ArrayList<>();
        }
        return realDatabase.getDatabases(user);
    }

    @Override
    public void createDatabase(User user, String name) {
        if (!hasAccess(user)) {
            System.out.println("Access denied: User does not have permission to create databases.");
            return;
        }
        else if (!isAuthenticated(user)) {
            System.out.println("Access denied: User is not authenticated.");
            return;
        }
        else if (DatabaseExists(user, name)) {
            System.out.println("Database already exists: " + name);
            return;
        }
        realDatabase.createDatabase(user, name);
    }

    @Override
    public void deleteDatabase(User user, String name) {
        if (!hasAccess(user)) {
            System.out.println("Access denied: User does not have permission to create databases.");
            return;
        }
        else if (!isAuthenticated(user)) {
            System.out.println("Access denied: User is not authenticated.");
            return;
        }
        else if (!DatabaseExists(user, name)) {
            System.out.println("Database does not exist: " + name);
            return;
        }
        realDatabase.deleteDatabase(user, name);
    }

    @Override
    public void query(User user, String sql) {
        if (!isAuthenticated(user)) {
            System.out.println("Access denied: User is not authenticated.");
            return;
        }
        else if (!hasAccess(user)) {
            System.out.println("Access denied: User does not have permission to query databases.");
            return;
        }
        realDatabase.query(user, sql);
    }

    @Override
    public void connect(User user) {
        realDatabase.connect(user);
    }

    @Override
    public void disconnect(User user) {
        if (!isAuthenticated(user)) {
            System.out.println("Access denied: User is not authenticated.");
            return;
        }
        realDatabase.disconnect(user);
    }
}
```

- before we call the methods from the service class we have to pass it through some verifications
- since the verifications will be done with the user that means we have to update the previous code to include the user 
	- an another solution would be to create the user inside the database so we dont have to constantly pass him as paramter

