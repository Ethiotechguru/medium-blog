# medium-blog```

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
        // private constructor to prevent outside instantiation`
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

Here’s an example of how the Command pattern works in code:
```c++
interface Command {
    void execute();
    void undo();
}

class Light {
    public void turnOn() {
        System.out.println("The light is on");
    }
    public void turnOff() {
        System.out.println("The light is off");
    }
}

class LightOnCommand implements Command {
    Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOn();
    }

    public void undo() {
        light.turnOff();
    }
}
```
In this example, we have an interface called Command which defines two methods: execute() and undo(). The LightOnCommand class is an implementation of the Command interface, it encapsulates the request of turning on a Light object by having a Light object as a property and calling the turnOn() method on it. It also has an undo() method that turns off the light.

This allows us to have a single point of control for executing commands, so we could have a remote control that holds an instance of this LightOnCommand and we can press the "on" button on the remote and it will call the execute() method on the LightOnCommand, this way we decoupled the actual execution of the command from the object that invoke it.

It also allows us to undo or redo the command by calling the undo() method.

In summary, the Command pattern is a way of encapsulating a request as an object, separating the execution of a command from the object that invokes it. It allows us to have a single point of control for executing commands, and it gives us the ability to undo or redo those commands. It also makes it easy to add new functionality, by creating new commands, without having to change the class that invoke it. This allows for flexibility, maintainability, and ease of modification of code, and it help to encapsulate the the what and the how of a command separately.
<hr>

### The Adapter pattern
The Adapter pattern is a design pattern that allows objects with incompatible interfaces to work together by wrapping one object with an adapter. This is useful when you have an existing class with a certain interface and you want to use that class in a context where a different interface is expected.

Here’s an example of how the Adapter pattern works in code:

```c++
interface AdvancedMediaPlayer {
    void playVlc(String fileName);
    void playMp4(String fileName);
}

class VlcPlayer implements AdvancedMediaPlayer {
    public void playVlc(String fileName) {
        System.out.println("Playing vlc file. Name: " + fileName);
    }

    public void playMp4(String fileName) {
        // do nothing
    }
}

interface MediaPlayer {
    void play(String audioType, String fileName);
}

class MediaAdapter implements MediaPlayer {
    AdvancedMediaPlayer advancedMusicPlayer;

    public MediaAdapter(String audioType) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMusicPlayer = new VlcPlayer();
        }
    }

    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMusicPlayer.playVlc(fileName);
        }
    }
}

class AudioPlayer implements MediaPlayer {
    MediaAdapter mediaAdapter;

    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing mp3 file. Name: " + fileName);
        } else if (audioType.equalsIgnoreCase("vlc")
                || audioType.equalsIgnoreCase("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media. " + audioType
                    + " format not supported");
        }
    }
}
```
In this example, we have the AdvancedMediaPlayer interface, which defines two methods for playing audio files, playVlc() and playMp4(). The VlcPlayer class is an implementation of AdvancedMediaPlayer that plays .vlc files. We also have the MediaPlayer interface, which defines a play() method that takes in the audio type and file name. The AudioPlayer class is an implementation of the MediaPlayer interface and it uses the MediaAdapter class to play audio files of other types, in this case, vlc files. The MediaAdapter class, takes in the audio type and creates an instance of the AdvancedMediaPlayer that can play that type of audio file, in this case, VlcPlayer, and it implements the play() method of the MediaPlayer interface by calling the appropriate method on the AdvancedMediaPlayer it holds an instance of.

This allows the AudioPlayer class to use the VlcPlayer class, which has a different interface, by wrapping it with the MediaAdapter class. This way it adapts the interface of the VlcPlayer class to match the interface expected by the AudioPlayer.

In summary, the Adapter pattern is a way of allowing objects with incompatible interfaces to work together.

### Facade pattern

The Facade pattern is a design pattern that provides a simplified interface to a complex system of objects, classes or subsystems. Think of it like the front of a building, the facade is the front side that you can see, but behind it, there are many rooms and systems working together. The facade pattern is similar, it provides a simplified interface that hides the complexity of the systems behind it.


In this example, the Computer class acts as a facade for a complex system of objects (CPU, Memory and HardDrive) by providing a simplified method startComputer() that the client can use to start the computer, this method hide the complexity of the system by calling methods on the objects of the subsystem. This way the client doesn't need to know the details of how the CPU, Memory and HardDrive work, it just needs to know how to start the computer.

Here’s an example of how the Facade pattern works in code:
```c++
class Computer {
    private CPU cpu;
    private Memory memory;
    private HardDrive hardDrive;
    
    public Computer() {
        this.cpu = new CPU();
        this.memory = new Memory();
        this.hardDrive = new HardDrive();
    }
    
    public void startComputer() {
        cpu.freeze();
        memory.load();
        hardDrive.read();
        cpu.jump();
        cpu.execute();
    }
}
```
Imagine you want to use your computer, but it has many different parts, like the CPU, memory, hard drive, and other components. Each of these parts has its own specific functions and complexities. To turn on your computer, you need to know how each part works, and how to make them all work together. The Facade pattern allows you to hide all of that complexity behind a single, simple interface, the power button. By pressing the power button, you don’t need to know how each part works, the facade (in this case, the computer) will take care of that for you.

In this example, the Computer class acts as a facade for a complex system of objects (CPU, Memory and HardDrive) by providing a simplified method startComputer() that the client can use to start the computer, this method hide the complexity of the system by calling methods on the objects of the subsystem. This way the client doesn't need to know the details of how the CPU, Memory and HardDrive work, it just needs to know how to start the computer.


The Template Method pattern
The Template Method pattern is a design pattern that defines the skeleton of an algorithm in a method, called the template method, and allows subclasses to redefine certain steps of the algorithm without changing its structure. Think of it like a recipe for making something, where the recipe defines the general steps for making the dish, but allows for variations in certain steps.

For example, let’s say we want to make a pizza, the template method could be the method that sets up the basic steps for making a pizza, like preparing the dough, adding the sauce, and baking the pizza. But, different types of pizza, like Margherita or Pepperoni, may have different ingredients added, like cheese or pepperoni. The template method allows subclasses to implement these specific steps while keeping the general steps consistent.

Here’s an example of how the Template Method pattern works in code:
```c++
abstract class Game {
    abstract void initialize();
    abstract void startPlay();
    abstract void endPlay();

    // template method
    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
}

class Cricket extends Game {
    @Override
    void endPlay() {
        System.out.println("Cricket Game Finished!");
    }

    @Override
    void initialize() {
        System.out.println("Cricket Game Initialized! Start playing.");
    }

    @Override
    void startPlay() {
        System.out.println("Cricket Game Started. Enjoy the game!");
    }
}
```

In this example, we have a Context class that can have multiple states represented by the State interface and different classes implements the State interface to represent different states. The Context class holds a reference to one of the state objects and it can change it's internal state by changing the reference to the state objects, we can call setState() method on the context to change it's state. The doAction() method is implemented by each state and it will behave differently depending on the state.

For example, if the Context class is in the StartState, when we call the doAction() method, it will print "Player is in start state". If we change the state to StopState and call the doAction() method again, it will print "Player is in stop state"

This allows the behavior of the Context class to change depending on its internal state, without changing its class.

An example in the real world, a vending machine, it can have multiple states, for example, idle, dispensing and sold out, each state would have its own behavior, like Idle state, it can accept money and change state to dispensing state, dispensing state will give the product to the customer and change state to Idle state or Sold out state, that won’t allow the customer to buy anything and will show an appropriate message.

```c++
class Context {
    private State state;

    public Context() {
        state = null;
    }

    public void setState(State state) {
        this.state = state;
    }

    public State getState() {
        return state;
    }
}
```

This pattern allows you to create a single class that represents multiple states and behaviors, instead of having a separate class for each state and behavior. This makes it easier to add new states and behaviors to the object without having to make changes to the object’s class. It also makes the code more flexible and maintainable because the different states and behaviors are separated out into separate classes.

In summary, The State pattern is a way to change the behavior of an object depending on its internal state, it separates the behavior of an object from the object itself, by creating separate objects for each state and the object holds a reference to one of these state objects. This allows the object to change its behavior without changing its class and makes the code more flexible and maintainable.



## Names
Abebe
Solomon
Samuel
Lilly
Maxine

## Countries
Hello Africa
Hello EThiopia
Hello America
Hello World

## Kebele
argoba kebele,
somo kebele
tomi kebele

# Cities In Washington State

- Seattle
- Lynnwood
- Bothle
- Bellevue
- Edmonds
- Redmond
- Woodnvill
- Mill Creek
- Mount Lake Terrece

