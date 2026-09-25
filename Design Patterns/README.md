# Design Patterns

---

Reference video: [https://youtu.be/rylaiB2uH2A?si=sWbku6vAopuUyrkz](https://youtu.be/rylaiB2uH2A?si=sWbku6vAopuUyrkz)

---

# Abstract VS Concrete

| Term | What it maps to |
| --- | --- |
| **Abstract** | ✅ Can be: |
| | • Interface (pure contract, no logic) |
| | • Abstract Class (contract + partial logic) |
| **Concrete** | ✅ Always: |
| | • Fully implemented Class |

---

## Object-Oriented Programming (OOP) Principles

- Encapsulation
- Abstraction
- Inheritance
- Polymorphism
- Coupling
- Composition

  ### Composition vs Inheritance

    **When to Use Composition:**

  - When you need more flexibility in constructing objects by assembling smaller, resusable, components.
  - When there is no clear “**is-a**” relationship between classes, and a “**has-a**” relationship is more appropriate.
  - When you want to avoid the limitations of inheritance, such as tight coupling and the **fragile base class problem [it is a topic]**

    **When to Use Inheritance:**

  - When there is a clear “**is-a**” relationship between classes, and subclass object can be related as instances of their superclass
  - When you want to promote code reuse by inheritance properties and behaviors from existing classes
  - When you want to leverage polymorphism to allow objects of different subclasses to be treated uniformly through their common superclass interface
    1. **Limited Extensibility**: The Fragile Base Class Problem limits the extensibility of software systems, as modifiers to the base class can become inscreasingly risky and costly over time. Developers may avoid making necessary changes due to the fear of breaking existing functionality — **Brittle Software**

  ### Fragile Base Class Problem and why you should use composition over inheritance

    The **Fragile Base Class Problem** is software design issue that arises in object-oriented programming when changes made to a base class can inadvertly break the functionality of derived classes. This problem occurs due to the tight coupling between base and derived classes inheritance hierarchies.

    1. **Inheritance Couping**: Inheritance create a strong coupling between the base class (superclass) and declare classes (subclass). Any changes made to the base class can potentially affect the behavior of all derived classes

    **MItigation Stratigies**: To mitigate the Fragile Base Class Problem, software developers can use design principles such as the **Open/Close Principle (OCP)** and **Dependency Inversion Principle (DIP)**, as well as design patterns like Composition vs Inheritance. These approaches promote loose coupling, encapsulation, the modular design, reducing the impact of changes in base classes

---

# UML

### Classes

![2025-06-21-005609_hyprshot.png](2025-06-21-005609_hyprshot.png)

### Inheritance Relationships

Dog **is a**n Animal

![2025-06-21-010213_hyprshot.png](2025-06-21-010213_hyprshot.png)

### Composition Relationship

Dog **has a** Size

![2025-06-21-011758_hyprshot.png](2025-06-21-011758_hyprshot.png)

### Association Relationship

Represented by an arrow

![2025-06-21-012619_hyprshot.png](2025-06-21-012619_hyprshot.png)

### Dependency Relationship

Represented by Dashed Arrow

![2025-06-21-012956_hyprshot.png](2025-06-21-012956_hyprshot.png)

- A class should have only one reason to change, meaning that is should have only one responsibility or purpose

---

# SOLID Principles

## S: Single Responsibility Principle (SRP)

## O: Open-Closed Principle (OCP)

- Software entities (classes, modules, functions, etc) should be open for extension but closed for modification

## L: Liskov Substitution Principle (LSP)

- Objects of superclass should be replacable with objects of its subclass without affecting the correctness of the program

## I: Interface Segretation Principle (ISP)

- Clients should not be forced to depend on interfaces they do not use

## D: Dependency Inversion Principle (DIP)

- High-level modules should not depend on low-level modules. Both should depend on abstractions

---

# Gang of Four (GOF) Design Patterns (23)

Three main groups of design patterns

### Creational Patterns

The different ways to create objects. Are a category of design patterns that focus on object creation, dealing with the best way to create objects whjile hiding the creation logic and making the system independent of how its object are created, composed, and represented  

1. Abstract Factory
    - is a creational design pattern that provides an interface for creating families of related objects without specifying their concrete classes, promoting encapsulation and allowing for the creation of object families that can vary independently
    - closely tied to strategy pattern but it controls how object behaves and factory pattern  is how object is created
2. Builder
    - is a deisgn pattern used to construct complex objects steps by step, providing clarity and flexibility in the creation process
    - essentiall making the class stand on its own with minial parameter inputs, leverating default values and filling up null holes that could possible cause errors

    ```jsx
    class Car {
      constructor(
        public engine: string,
        public seats: number,
        public gps: boolean,
        public sunroof: boolean,
        public autopilot?: boolean
      ) {}
    }
    
    class CarBuilder {
      private engine = 'Default';
      private seats = 4;
      private gps = false;
      private sunroof = false;
      private autopilot = false;
    
      setEngine(engine: string) { this.engine = engine; return this; }
      setSeats(seats: number) { this.seats = seats; return this; }
      enableGPS() { this.gps = true; return this; }
      enableSunroof() { this.sunroof = true; return this; }
      enableAutopilot() { this.autopilot = true; return this; }
    
      build(): Car {
        return new Car(this.engine, this.seats, this.gps, this.sunroof, this.autopilot);
      }
    }
    
    // Usage:
    const myCar = new CarBuilder()
      .setEngine('V8')
      .enableGPS()
      .enableAutopilot()
      .build();
    
    ```

3. Factory Method
    - is a creational design pattern that defines an interface for creating objects, but allows subclasses to alter the type of objects that will be created, providing a way to delegate the instantiation logic to subclasses, enabling flexibility in object creation withouth changing the client code

        ```jsx
        interface Product {
          operation(): void;
        }
        
        class ConcreteProductA implements Product {
          operation() { console.log("A"); }
        }
        
        class ConcreteProductB implements Product {
          operation() { console.log("B"); }
        }
        
        abstract class Creator {
          abstract factoryMethod(): Product;
        
          someOperation(): void {
            const product = this.factoryMethod();
            product.operation();
          }
        }
        
        class ConcreteCreatorA extends Creator {
          factoryMethod(): Product {
            return new ConcreteProductA();
          }
        }
        
        class ConcreteCreatorB extends Creator {
          factoryMethod(): Product {
            return new ConcreteProductB();
          }
        }
        ```

    - **vague**
4. Prototype
    - is a creational design pattern that allows object to be copied or cloned, providing a mechanism to create new instances by copying existing objects without explicitly invoking their constructors, and it is used to efficiently produce new instances with identical properties to existing objects
    - basically create new objects by copying an existing object (prototype), instead of instantiating from scratch
5. Singleton
    - is a creational design pattern that ensures a class has only one instance and provides a global point of access to the instance . The single intance is commonly used for managing shared resourced, configuration settings, or logging functionality within the aplication
    - basically existed on program bootstrap until program termination

## 2. Structural Patterns

The relationships between thos objects. Focuses on the composition of classes and objects to form larger structures and systems. These patterns primarly deal with how classes and objects can be combined to form a larger, more complex structures while keeping these structures flexible and efficient. The key objective of structural design patterns is to provide solutions to design problems related to object composition and structure, allowing for better organization and management of code

1. **Adapter**
    - is a structual design pattern that allows incopatible interfaces between classes to work together by providing a **wrapper (object)** that translates one interface into another
        - Target Interface (Abstract Interface)
        - Adapter (Concrete Class wrapper )
        - Adaptee (Concrete Class)

    3 Common Adapter Types

    | Type | Description |
    | --- | --- |
    | **Class Adapter** | Inheritance-based (C#, Java — rarely in TS) |
    | **Object Adapter** | Composition-based (most common in TypeScript, JS, Python) |
    | **Two-Way Adapter** | Allows translation both directions |

    1. **Bridge**
        - is a design pattern that seperates a large class, or a set of related into two seperate hierarchies so that they can develop independently from each other

        ![2025-06-22-141035_hyprshot.png](2025-06-22-141035_hyprshot.png)

    | Term | Meaning | Notes |
    | --- | --- | --- |
    | **Component (Interface / Base class)** | The common interface for all objects in the hierarchy | Allows uniform treatment |
    | **Leaf** | The simplest object, no children | Ex: Button, File, Fuel Tank |
    | **Composite (Composite Node)** | An object that holds children Components | Ex: Panel, Folder, Rocket Stage |
    | **Parent Composite** | Composite node higher in the hierarchy | Ex: Entire UI screen, Entire Ship |
    | **Child** | Sub-object inside a Composite | |
    | **Uniform Interface** | All objects (Leaf or Composite) expose the same operations | e.g., `.render()`, `.calculateCost()`, `.display()` |
    | **Recursive Composition** | Composites may contain other Composites | Allows deeply nested structures |
    | **Operation Delegation** | Composite calls operation on its children | Ex: `forEach(child -> child.render())` |
    | **Part-Whole Hierarchy** | Structural way of thinking: whole made of parts | Composite = Whole, Leaf = Part |
    | **Transparency** | Clients don't need to know if they deal with leaf or composite | Always call `.operation()` |

2. **Composite**
    - is a structural design pattern that enables the creation of tree-like structures to represent collections of object, where both individual objects and groups of objects are treated in a unified manner

        ![2025-06-22-131638_hyprshot.png](2025-06-22-131638_hyprshot.png)

    Advance Terms

    | Term | Meaning | Notes |
    | --- | --- | --- |
    | **Structural Recursion** | The recursive nature of traversing the tree | Used heavily in rendering trees, scene graphs |
    | **Aggregate** | Synonym sometimes used for Composite node | Often used in DDD world |
    | **Hierarchy Depth** | The levels of nesting | |
    | **Root Composite** | The very top-level composite node | Ex: AppModule, Root Scene, Root Folder |
    | **Traversal Order** | How you process children (depth-first, breadth-first) | Important in certain algorithms |
    | **Visitor Friendly** | Composite trees often work well with Visitor Pattern | Because you can traverse them uniformly |

3. **Decorator**
    - is a structual design pattern that allows behavior to be added to individual objects dynamically, enhancing functionality without altering the object’s structure, and it’s used to extend or modify the behavior of objects by wrapping them with additional functionality through composition
    - You take existing behavior → wrap it → add something → still delegate original behavior.

        ```jsx
        // in simple terms
        decoratedFunction(input) {
          // new behavior BEFORE
          originalFunction(input)
          // new behavior AFTER
        }
        ```

4. **Facade**
    - is a structural design pattern the provides a simplified interface to a complex system, encapsulating the complexities of multiple subsystems into a single unified inteface for clients
    - Basically KOISK that hides internal implementaion (order⇒call api⇒response)
5. **Flyweight**
    - is a structual design pattern that aims to minimize memory usage by sharing common state between multiple objects, allowing efficient handling of large numbers of lightweight objects with shared characteristics
    - is performance based conceptial tool
    - Blender Technology Example about **instancing**
6. **Proxy**
    - is a structual pattern that provides a proxy, agent, or object to control access to another object, allowing for additional functionality such as caching, logging, lazy loading, or access control, without changing client’s code
    - Delegation ⇒ Control ⇒ Interception ⇒ Access control ⇒ Caching ⇒ Lazy loading

        | Use Case | Type |
        | --- | --- |
        | **Lazy loading** | Virtual Proxy |
        | **Access control** | Protection Proxy |
        | **Remote objects** | Remote Proxy (RPC / gRPC) |
        | **Logging / Metrics** | Logging Proxy |
        | **Caching** | Cache Proxy |
        | **Security layer** | Firewall Proxy |

## 3. Behavioural Patterns

The interaction or communication between those objects

1. **Chain Responsibility**
    - allows building a chain of objects to handle a request. A request is passed through is passed through a chain of handlers, each capable of either handling the request or passing it to the next handler in the chain
2. **Command**
    - is a behavioral pattern that encapsulates a request as an object, allowing you to paramterized clients with queues, request or operations, it enables you to decouple the sender from the receiver, providing flexibility in the execution of commands and supporting undoable operations
    - You separate **what needs to be done** (the command) from **who triggers it** (the invoker) and **who receives it** (the receiver).

        MMO reference (concerns SRP and Polymorphism the most)

        - Invoker (Buff creator)
        - Command (Buff)
        - Reciever (Player)
3. **Interpreter**
    - defines a way to represent and evaluate sentences in a language by using an abstract class for expressions, which concrete subclasses implement to interpret specific parts of the language’s grammar
    - is probably the most complex and least used of the GoF design patterns
        - **Abstract Expression:** Establishes the interface for all expressions within the language.

        **The Components of the Interpreter Pattern:**

        - **Terminal Expression:** Represents the fundamental components of the Language, such as numbers or variables.
        - **Non-terminal Expression:** Represents more complex expressions that are composed of other expressions using operators or functions.
        - **Interpreter:** Implements the logic for interpretation and determines how to evaluate different types of expressions
4. **Iterator**
    - provides a way of iterating over an object without having to expose the object’s internal structure, which may change in the future, changing the internals of an object should not affect its consumer s
        - Collection
        - Iterator
        - Concrete Iterators
5. **Mediator**
    - defines an object (the Mediator) that describes how set of objects interface with each other, therefore reducing lots of chaotic dependencies between those objects

        NestJS for refence

        - commands/
        - queries/
        - CQRS (npm package and architectural approach)
6. **Memento**
    - is used to restore an object to a previous state, concerns about undo/redo or snapshots
        - Originator (
        - Memento (State)
        - Caretaker (History)
7. **Observer**
    - involves an object, known as the subject, maintaining a list of its dependent objects, called observers, and notifying them automatically of any state changes
    - is **AKA pub and subscribe or Publish and Subscribe (Pub/Sub):** the **subject (publisher)** publishes changes in its state, and the **subscriber (observers)** subscribes to that events
        - Subject (Abstract Class)
        - Observer (Interface)
        - Concrete Observers (Collection)
8. **State**
    - allows am object to behave differently depending on the state that is in
        - Context (Base Class
        - Interface (State)
        - Concrete States
9. **Strategy**
    - is used to pass different algorithms, or behavoirs, into an object
    - consider an application that stores videos, before storing a video. the video needs to be compressed using a specific compression algorithm, such as MOV or MP3, then, if neccessary, apply an overlay to the video, such as black and white or blur, different options of algorithms that are needed are then put into objects for flexible usage via abstractions into strategy layer
10. **Template Method**
    - allows you to define a template method, or skeleton, for an operation, the specific steps can be implemented in subclasses
        - Beverage Maker (Superclass)
        - Beverage (Interface)
        - Tea (Concrete Classes)
11. **Visitor**
    - seperates the algorithms, or behavoirs, from the objects on which they operate

---

# Video TimeStamps

([0:00:00](https://www.youtube.com/watch?v=rylaiB2uH2A)) Intro
([0:00:33](https://www.youtube.com/watch?v=rylaiB2uH2A&t=33s)) Course contents
([0:01:34](https://www.youtube.com/watch?v=rylaiB2uH2A&t=94s)) Gang of Four design patterns
([0:02:39](https://www.youtube.com/watch?v=rylaiB2uH2A&t=159s)) What are design patterns & why learn them?
([0:05:38](https://www.youtube.com/watch?v=rylaiB2uH2A&t=338s)) Course prerequisites
([0:06:57](https://www.youtube.com/watch?v=rylaiB2uH2A&t=417s)) About me
([0:07:32](https://www.youtube.com/watch?v=rylaiB2uH2A&t=452s)) Book version
([0:08:19](https://www.youtube.com/watch?v=rylaiB2uH2A&t=499s)) Code repo
([0:08:49](https://www.youtube.com/watch?v=rylaiB2uH2A&t=529s)) Setup
([0:12:19](https://www.youtube.com/watch?v=rylaiB2uH2A&t=739s)) OOP concepts intro
([0:12:42](https://www.youtube.com/watch?v=rylaiB2uH2A&t=762s)) Encapsulation - OOP
([0:25:48](https://www.youtube.com/watch?v=rylaiB2uH2A&t=1548s)) Abstraction - OOP
([0:30:52](https://www.youtube.com/watch?v=rylaiB2uH2A&t=1852s)) Inheritance - OOP
([0:36:40](https://www.youtube.com/watch?v=rylaiB2uH2A&t=2200s)) Polymorphism - OOP
([0:45:04](https://www.youtube.com/watch?v=rylaiB2uH2A&t=2704s)) Coupling - OOP
([0:55:17](https://www.youtube.com/watch?v=rylaiB2uH2A&t=3317s)) Composition - OOP
([0:58:11](https://www.youtube.com/watch?v=rylaiB2uH2A&t=3491s)) Composition vs inheritance - OOP
([1:01:00](https://www.youtube.com/watch?v=rylaiB2uH2A&t=3660s)) Fragile base class problem - OOP
([1:05:24](https://www.youtube.com/watch?v=rylaiB2uH2A&t=3924s)) UML
([1:14:01](https://www.youtube.com/watch?v=rylaiB2uH2A&t=4441s)) SOLID intro
([1:15:01](https://www.youtube.com/watch?v=rylaiB2uH2A&t=4501s)) S - SOLID
([1:21:26](https://www.youtube.com/watch?v=rylaiB2uH2A&t=4886s)) O - SOLID
([1:32:20](https://www.youtube.com/watch?v=rylaiB2uH2A&t=5540s)) L - SOLID
([1:45:20](https://www.youtube.com/watch?v=rylaiB2uH2A&t=6320s)) I - SOLID
([1:54:10](https://www.youtube.com/watch?v=rylaiB2uH2A&t=6850s)) D - SOLID
([2:04:56](https://www.youtube.com/watch?v=rylaiB2uH2A&t=7496s)) Design patterns intro
([2:05:35](https://www.youtube.com/watch?v=rylaiB2uH2A&t=7535s)) Behavioural design patterns
([2:07:37](https://www.youtube.com/watch?v=rylaiB2uH2A&t=7657s)) Memento pattern - behavioural
([2:33:40](https://www.youtube.com/watch?v=rylaiB2uH2A&t=9220s)) State pattern - behavioural
([3:00:27](https://www.youtube.com/watch?v=rylaiB2uH2A&t=10827s)) Strategy pattern - behavioural
([3:26:47](https://www.youtube.com/watch?v=rylaiB2uH2A&t=12407s)) Iterator pattern - behavioural
([3:46:09](https://www.youtube.com/watch?v=rylaiB2uH2A&t=13569s)) Command pattern - behavioural
([4:24:17](https://www.youtube.com/watch?v=rylaiB2uH2A&t=15857s)) Template method pattern - behavioural
([4:56:50](https://www.youtube.com/watch?v=rylaiB2uH2A&t=17810s)) Observer pattern - behavioural
([5:31:20](https://www.youtube.com/watch?v=rylaiB2uH2A&t=19880s)) Mediator pattern - behavioural
([6:10:19](https://www.youtube.com/watch?v=rylaiB2uH2A&t=22219s)) Chain of responsibility pattern - behavioural
([6:42:55](https://www.youtube.com/watch?v=rylaiB2uH2A&t=24175s)) Visitor pattern - behavioural
([7:06:29](https://www.youtube.com/watch?v=rylaiB2uH2A&t=25589s)) Interpreter pattern - behavioural
([7:38:53](https://www.youtube.com/watch?v=rylaiB2uH2A&t=27533s)) Structural design patterns intro
([7:40:32](https://www.youtube.com/watch?v=rylaiB2uH2A&t=27632s)) Composite pattern - structural
([7:56:09](https://www.youtube.com/watch?v=rylaiB2uH2A&t=28569s)) Adapter pattern - structural
([8:13:26](https://www.youtube.com/watch?v=rylaiB2uH2A&t=29606s)) Bridge pattern - structural
([8:33:16](https://www.youtube.com/watch?v=rylaiB2uH2A&t=30796s)) Proxy pattern - structural
([8:51:33](https://www.youtube.com/watch?v=rylaiB2uH2A&t=31893s)) Flyweight pattern - structural
([9:15:25](https://www.youtube.com/watch?v=rylaiB2uH2A&t=33325s)) Facade pattern - structural
([9:27:13](https://www.youtube.com/watch?v=rylaiB2uH2A&t=34033s)) Decorator pattern - structural
([9:55:16](https://www.youtube.com/watch?v=rylaiB2uH2A&t=35716s)) Creational design patterns intro
([9:58:50](https://www.youtube.com/watch?v=rylaiB2uH2A&t=35930s)) Prototype pattern - creational
([10:19:13](https://www.youtube.com/watch?v=rylaiB2uH2A&t=37153s)) Singleton pattern - creational
([10:37:44](https://www.youtube.com/watch?v=rylaiB2uH2A&t=38264s)) Factory method pattern - creational
([10:55:03](https://www.youtube.com/watch?v=rylaiB2uH2A&t=39303s)) Abstract factory pattern - creational
([11:12:26](https://www.youtube.com/watch?v=rylaiB2uH2A&t=40346s)) Builder pattern - creational
([11:46:29](https://www.youtube.com/watch?v=rylaiB2uH2A&t=42389s)) Course conclusion
