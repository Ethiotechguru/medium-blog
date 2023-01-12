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
Here’s an example of how the Factory pattern works in code:

```c++
class CarFactory {
    public static Car createCar(String type) {
        if (type.equals("sedan")) {
            return new Sedan();
        } else if (type.equals("truck")) {
            return new Truck();
        } else {
            return null;
        }
    }
}

class Sedan extends Car {
    // class implementation
}

class Truck extends Car {
    // class implementation
}
```
In this example, the CarFactory class has a public static method called *createCar()*, which takes in a String as a parameter called type. Depending on the value of the type parameter, the *createCar()* method creates and returns an instance of either the Sedan class or the Truck class, both classes are inherited from the Car class.

This way of creating objects is very helpful because it decouples the code that creates the objects from the classes of the objects being created. So in the example, if we want to add a new type of car (let’s say “SUV”) the code that uses the factory doesn’t have to change, just the factory itself. This allows for flexibility, maintainability, and ease of modification of code.

In summary, The Factory pattern is a way of creating objects without specifying the class of objects. The factory takes the responsibility of creating objects based on certain inputs and conditions, thus providing a way to create objects that conform to an interface or a base class while allowing the implementation details of the actual classes to be hidden. It’s a way to separate the object creation process from the code that uses the objects and it provide a clear and maintainable way to create objects, especially when the class of objects may change over time.

<hr>

### The Observer pattern
The Observer pattern is a design pattern that allows objects to be notified of changes to other objects. This is useful when you have multiple objects that need to be updated when something changes in another object, and you want to avoid tight coupling between the objects.

Here’s an example of how the Observer pattern works in code:

```C++
class WeatherData {
    private List<Observer> observers;
    private float temperature;
    private float humidity;
    private float pressure;

    public WeatherData() {
        observers = new ArrayList<Observer>();
    }

    public void registerObserver(Observer o) {
        observers.add(o);
    }

    public void removeObserver(Observer o) {
        int i = observers.indexOf(o);
        if (i >= 0) {
            observers.remove(i);
        }
    }

    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(temperature, humidity, pressure);
        }
    }

    public void measurementsChanged() {
        notifyObservers();
    }

    public void setMeasurements(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        measurementsChanged();
    }
}
```

In this example, the WeatherData class has a list of observers, which are objects that have registered to be notified when the weather data changes. The *registerObserver()* method is used to add new observers to the list, and the *removeObserver()* method is used to remove them. The *notifyObservers()* method is used to notify all the observers in the list when the weather data changes. When measurements changes (e.g. the temperature or the humidity changes) WeatherData class use *measurementsChanged()* method to notify all the observers by calling *notifyObservers()* method, each observer have an *update()* method that get triggered by the call and it would update the observer with the new measurements.

This way, the WeatherData class and the observer classes are loosely coupled, meaning that they don't depend on each other in a specific way. The observer classes only need to implement the update() method, and the WeatherData class only needs to know that the observers have this method. This allows for flexibility, maintainability, and ease of modification of code.

In summary, the Observer pattern is a way of allowing objects to be notified of changes to other objects. It provides a way for objects to communicate with each other without being tightly coupled, which means that objects don’t need to know the details of how other objects work. It’s a way to enable one-to-many communication and to decouple the objects that trigger an event from the objects that respond to it, This allows for flexibility and reusability, as well as ease of modification of the code.
<hr>

### The Decorator pattern
It is a design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. This is useful when you want to add new features to an object without changing its class or when you want to add features to an object at runtime.

Here’s an example of how the Decorator pattern works in code:
```c++
abstract class Beverage {
    protected String description = "Unknown Beverage";
    public String getDescription() {
        return description;
    }
    public abstract double cost();
}

class Espresso extends Beverage {
    public Espresso() {
        description = "Espresso";
    }
    public double cost() {
        return 1.99;
    }
}

abstract class CondimentDecorator extends Beverage {
    public abstract String getDescription();
}

class Mocha extends CondimentDecorator {
    Beverage beverage;
    public Mocha(Beverage beverage) {
        this.beverage = beverage;
    }
    public String getDescription() {
        return beverage.getDescription() + ", Mocha";
    }
    public double cost() {
        return .20 + beverage.cost();
    }
}
```
<hr>

### The Command pattern
The Command pattern is a design pattern that encapsulates a request as an object, separating the execution of a command from the object that invokes it. This is useful when you want to have a single point of control for executing commands and when you want to be able to undo or redo those commands.
