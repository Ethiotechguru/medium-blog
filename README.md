# medium-blog
OOP Design pattern blog for medium.com
## OOP Design Pattern
**Object-oriented** design patterns are a way to solve common programming problems that developers face when designing software. There are many different design patterns, and each one has a specific purpose and solves a specific problem. Here are a few common ones:
<hr>

## Most common Design Patters Explained

### The Singleton pattern
The Singleton pattern is a design pattern that ensures that a class has only one instance (or object) at any given time, while providing a global access point to that instance. This is useful in situations where you only want one object of a certain class to exist, such as when you have a single database connection or a single configuration object.
Here’s an example of how the Singleton pattern works in code:
```C++ 
class DatabaseConnection {
    private static DatabaseConnection instance;

    private DatabaseConnection() {
        // private constructor to prevent outside instantiation
    }

    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }

    // other methods for working with the database connection go here
}
```
In this example, the *DatabaseConnection* class has a private constructor, which prevents outside code from instantiating it. The only way to create an instance of the class is by calling the *getInstance()* method, which is a static method. If an instance of the class has not been created yet, the *getInstance()* method creates one and assigns it to the instance variable. If an instance has already been created, the *getInstance()* method simply returns the existing instance.
<hr>

### The Factory pattern
The Factory pattern is a design pattern that helps to create objects without specifying the exact class of object that will be created. This is useful when you want to create objects based on some input or condition, but you don’t want the code that creates the objects to know the specific details of how the objects are created.
<hr>

### The Observer pattern
The Observer pattern is a design pattern that allows objects to be notified of changes to other objects. This is useful when you have multiple objects that need to be updated when something changes in another object, and you want to avoid tight coupling between the objects.
<hr>

### The Decorator pattern
It is a design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. This is useful when you want to add new features to an object without changing its class or when you want to add features to an object at runtime.
<hr>

### The Command pattern
The Command pattern is a design pattern that encapsulates a request as an object, separating the execution of a command from the object that invokes it. This is useful when you want to have a single point of control for executing commands and when you want to be able to undo or redo those commands.