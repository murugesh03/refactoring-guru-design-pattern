# Dive Into Design Patterns — Complete Reference

## Table of Contents

1. [Introduction to OOP](#introduction-to-oop)
   - [Basics of OOP](#basics-of-oop)
   - [Pillars of OOP](#pillars-of-oop)
   - [Relations Between Objects](#relations-between-objects)
2. [Introduction to Design Patterns](#introduction-to-design-patterns)
   - [What's a Design Pattern?](#whats-a-design-pattern)
   - [Why Should I Learn Patterns?](#why-should-i-learn-patterns)
3. [Software Design Principles](#software-design-principles)
   - [Features of Good Design](#features-of-good-design)
   - [Encapsulate What Varies](#encapsulate-what-varies)
   - [Program to an Interface, not an Implementation](#program-to-an-interface-not-an-implementation)
   - [Favor Composition Over Inheritance](#favor-composition-over-inheritance)
   - [SOLID Principles](#solid-principles)
4. [Creational Patterns](#creational-design-patterns)
   - [Factory Method](#factory-method)
   - [Abstract Factory](#abstract-factory)
   - [Builder](#builder)
   - [Prototype](#prototype)
   - [Singleton](#singleton)
5. [Structural Patterns](#structural-design-patterns)
   - [Adapter](#adapter)
   - [Bridge](#bridge)
   - [Composite](#composite)
   - [Decorator](#decorator)
   - [Facade](#facade)
   - [Flyweight](#flyweight)
   - [Proxy](#proxy)
6. [Behavioral Patterns](#behavioral-design-patterns)
   - [Chain of Responsibility](#chain-of-responsibility)
   - [Command](#command)
   - [Iterator](#iterator)
   - [Mediator](#mediator)
   - [Memento](#memento)
   - [Observer](#observer)
   - [State](#state)
   - [Strategy](#strategy)
   - [Template Method](#template-method)
   - [Visitor](#visitor)
7. [Conclusion](#conclusion)

---

## Introduction to OOP

### Basics of OOP

Object-oriented programming (OOP) is a paradigm based on wrapping pieces of data and related behavior into special bundles called **objects**, constructed from blueprints called **classes**.

**Objects & Classes**

- A **class** is like a blueprint that defines the structure for objects.
- An **object** is a concrete instance of a class.
- **Fields** (attributes) store data — these represent the object's *state*.
- **Methods** define behavior.
- Together, fields and methods are called *members* of a class.

Example: `Oscar` is an object (instance) of the `Cat` class. Every cat shares the same attributes (`name`, `sex`, `age`, `color`, `weight`) but has different values for each.

**Class Hierarchies**

- A **superclass** (parent) contains shared attributes and behaviors.
- **Subclasses** (children) inherit state and behavior from the parent and only define what differs.
- Subclasses can override parent methods — either completely replacing or enhancing the default behavior.

Example: `Cat` and `Dog` both extend `Animal`. `Animal` extends `Organism`.

---

### Pillars of OOP

**1. Abstraction**

A model of a real-world object, limited to a specific context. Only relevant details are represented; the rest is omitted.

> An `Airplane` class in a flight simulator focuses on flight data. In a booking app, it focuses on seat maps.

**2. Encapsulation**

Hiding an object's internal details behind a well-defined interface. Only the public API is exposed.

> Like a car — you interact through the steering wheel and pedals, not the engine internals.

Each object has:
- **Interface** — the public part (open to interaction)
- **Private state/implementation** — hidden from the outside

**3. Inheritance**

The ability to build new classes on top of existing ones, enabling code reuse.

- A subclass has the same interface as its parent — you cannot hide a method that was declared in the superclass.
- In most languages, a class can extend only **one** superclass, but can implement **multiple** interfaces.
- Abstract methods force subclasses to provide their own implementations.

**4. Polymorphism**

The ability of a program to detect the real class of an object and call its implementation even when its real type is unknown in the current context.

```
bag = [new Cat(), new Dog()]
foreach (Animal a : bag)
  a.makeSound()
// Output: Meow! Woof!
```

Objects can "pretend" to be something else — usually the class they extend or the interface they implement.

---

### Relations Between Objects

| Relation | Description | UML Notation |
|---|---|---|
| **Association** | One object uses or interacts with another. A permanent link (field reference). | Simple arrow |
| **Dependency** | Weaker than association. One object accepts another as a method parameter or instantiates it temporarily. | Dashed arrow |
| **Composition** | "Whole-part" relationship. The component **can only exist** as part of the container. | Solid diamond (filled) |
| **Aggregation** | Like composition but looser. The component can exist independently and be linked to multiple containers. | Solid diamond (hollow) |

---

## Introduction to Design Patterns

### What's a Design Pattern?

Design patterns are **typical solutions to commonly occurring problems** in software design. They are like pre-made blueprints that you customize to solve a recurring design problem.

- A pattern is **not** a specific piece of code — it's a general concept for solving a particular problem.
- Patterns differ from algorithms: an algorithm defines a clear set of actions; a pattern is a high-level description of a solution.

**What does a pattern consist of?**

- **Intent** — briefly describes the problem and solution
- **Motivation** — explains the problem and the solution in depth
- **Structure** — shows each part of the pattern and how they relate
- **Code example** — in a popular programming language

**Classification of Patterns**

- **Idioms** — low-level, apply to a single language
- **Architectural patterns** — high-level, universal, used to design whole applications
- By intent:
  - **Creational** — object creation mechanisms for flexibility and reuse
  - **Structural** — assembling objects/classes into larger structures
  - **Behavioral** — effective communication and responsibility between objects

**Who invented patterns?**

Christopher Alexander described the concept in *A Pattern Language* (1977). In 1995, Erich Gamma, John Vlissides, Ralph Johnson, and Richard Helm published *Design Patterns: Elements of Reusable Object-Oriented Software* (the "GoF book") featuring 23 patterns.

---

### Why Should I Learn Patterns?

- Patterns are a **toolkit of tried and tested solutions** to common problems.
- They teach you how to solve all sorts of problems using principles of OOP.
- Patterns define a **common language** between developers. Saying "use a Singleton" is faster than explaining it from scratch.

---

## Software Design Principles

### Features of Good Design

**Code Reuse**

- Using design patterns is one way to increase flexibility and make components easier to reuse.
- There are three levels of reuse:
  - **Lowest** — classes (single classes, containers, iterators)
  - **Highest** — frameworks (define the architecture, you fill in the gaps)
  - **Middle (patterns)** — less risky than frameworks, reuse design ideas independently of concrete code

**Extensibility**

Change is the only constant. Software must accommodate:
- New target platforms
- New UI requirements
- New business features

All seasoned developers design with future changes in mind.

---

### Encapsulate What Varies

> *Identify the aspects of your application that vary and separate them from what stays the same.*

The main goal is to **minimize the effect caused by changes**.

**Method-level example:**

Extract tax calculation logic (which changes often) out of `getOrderTotal()` into its own `getTaxRate(country)` method. Tax-related changes become isolated.

**Class-level example:**

Move `TaxCalculator` logic out of the `Order` class into a dedicated `Tax` class. The `Order` class delegates tax work to this object.

---

### Program to an Interface, not an Implementation

> *Program to an interface, not an implementation. Depend on abstractions, not on concrete classes.*

Steps to apply:
1. Determine what one object needs from the other (which methods it calls).
2. Describe these methods in a new interface or abstract class.
3. Make the dependency class implement this interface.
4. Make the second class depend on the **interface** rather than the concrete class.

**Company example:**

Instead of `Company` being tightly coupled to `Designer` and `Programmer` classes, extract an `Employee` interface. Then `Company` can work with any employee type via polymorphism. To decouple further, make `getEmployees()` abstract in `Company` so each subclass creates its own type of employee — this is a preview of the **Factory Method** pattern.

---

### Favor Composition Over Inheritance

**Problems with inheritance:**

- A subclass can't reduce the interface of the superclass — you must implement all abstract methods.
- Overridden methods must remain compatible with the base class behavior.
- Inheritance breaks encapsulation — internal parent details become visible to subclasses.
- Subclasses are tightly coupled to superclasses.
- Leads to **parallel inheritance hierarchies** and combinatorial explosion.

> A car + engine type + navigation type = tons of subclass combinations.

**Composition** ("has a" relationship) to the rescue:

Instead of inheriting behavior, delegate it to other objects. You can swap these objects at runtime.

> This structure resembles the **Strategy** pattern.

---

### SOLID Principles

Introduced by Robert Martin in *Agile Software Development, Principles, Patterns, and Practices*.

#### S — Single Responsibility Principle

> *A class should have just one reason to change.*

Each class should be responsible for a single part of the functionality, with that responsibility entirely encapsulated within the class.

- Too many responsibilities means changing one thing risks breaking another.
- **Example:** Extract `TimesheetReport` printing logic from `Employee` class into a separate `TimesheetReporter` class.

#### O — Open/Closed Principle

> *Classes should be open for extension but closed for modification.*

- **Open** for extension: you can produce subclasses and add new methods/fields.
- **Closed** for modification: the existing interface is stable.

- **Example:** Instead of modifying `Order` to add new shipping methods, extract a `Shipping` interface. New shipping methods are new classes implementing that interface — no changes to `Order`.

#### L — Liskov Substitution Principle

> *When extending a class, you should be able to pass objects of the subclass in place of objects of the parent class without breaking the client code.*

Formal checklist:
- **Parameter types** in subclass methods should match or be **more abstract** than in the superclass.
- **Return types** in subclass methods should match or be a **subtype** of the superclass return type.
- Subclass methods **should not throw** exception types that the base method doesn't expect.
- A subclass **should not strengthen pre-conditions** (require more from callers).
- A subclass **should not weaken post-conditions** (promise less to callers).
- **Invariants** of the superclass must be preserved.
- A subclass should not change values of private fields of the superclass.

**Example violation:** `ReadOnlyDocument` overrides `save()` to throw an exception — clients that expect any `Document` can call `save()` break. Fix: make `ReadOnlyDocument` the base class; `WritableDocument` is the subclass that adds saving.

#### I — Interface Segregation Principle

> *Clients shouldn't be forced to depend on methods they do not use.*

Break "fat" interfaces into more granular, specific ones.

**Example:** A cloud library with one huge interface covering all cloud services. Providers that only support some services shouldn't be forced to implement everything. Break the interface into smaller ones (`StorageProvider`, `ComputeProvider`, etc.).

Keep the balance — don't over-divide.

#### D — Dependency Inversion Principle

> *High-level classes shouldn't depend on low-level classes. Both should depend on abstractions. Abstractions shouldn't depend on details. Details should depend on abstractions.*

Steps:
1. Declare interfaces for low-level operations in **business terms**.
2. Make high-level classes depend on those interfaces (not concrete low-level classes).
3. Low-level classes implement the interfaces and become dependent on the business logic level — reversing the dependency direction.

**Example:** A `BudgetReport` class depends on a `MySQLDatabase` class directly. Fix: create a `Database` interface. `BudgetReport` depends on `Database`. `MySQLDatabase` implements `Database`. If the DB changes, only `MySQLDatabase` changes — `BudgetReport` is unaffected.

---

## Creational Design Patterns

Creational patterns provide object creation mechanisms that increase flexibility and reuse of existing code.

---

### Factory Method

> Also known as: **Virtual Constructor**

**Intent:** Provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

---

**Problem**

A logistics app tightly coupled to a `Truck` class. When sea transport is needed, the entire codebase must change. Adding each new transport type requires changing existing code everywhere.

**Solution**

Replace direct object construction (`new Truck()`) with calls to a **factory method**. Subclasses override the factory method to return different product types. The client only uses the common `Transport` interface (e.g., `deliver()`).

---

**Structure**

1. **Product** — declares the common interface (`Transport` with `deliver()`)
2. **Concrete Products** — `Truck`, `Ship` implementing the interface
3. **Creator** — declares the abstract factory method; contains core business logic
4. **Concrete Creators** — `RoadLogistics`, `SeaLogistics` — override the factory method

---

**Pseudocode Example** (Cross-platform UI)

```pseudocode
abstract class Dialog
  abstract method createButton(): Button
  method render()
    button = createButton()
    button.onClick(closeDialog)
    button.render()

class WindowsDialog extends Dialog
  method createButton(): Button
    return new WindowsButton()

class WebDialog extends Dialog
  method createButton(): Button
    return new HTMLButton()

interface Button
  method render()
  method onClick(f)
```

---

**Applicability**

- When you don't know the exact types/dependencies of objects your code needs at design time.
- When you want to provide users of a library a way to extend its internal components.
- When you want to save resources by reusing existing objects (object pool pattern).

**How to Implement**

1. Make all products follow the same interface.
2. Add an empty factory method inside the creator class.
3. Replace product constructor calls with factory method calls.
4. Create subclasses for each product type and override the factory method.
5. If base factory method is now empty, make it abstract.

**Pros**
- Avoids tight coupling between creator and concrete products.
- Single Responsibility: product creation in one place.
- Open/Closed: introduce new products without breaking existing code.

**Cons**
- More subclasses required — increased complexity.

**Relations with Other Patterns**
- Evolves toward Abstract Factory, Prototype, or Builder.
- Abstract Factory classes are often based on a set of Factory Methods.
- Can use Factory Method along with Iterator.
- Factory Method is a specialization of Template Method.

---

### Abstract Factory

**Intent:** Lets you produce **families of related objects** without specifying their concrete classes.

---

**Problem**

A furniture shop needs to create families of products (`Chair`, `Sofa`, `CoffeeTable`) in multiple variants (`Modern`, `Victorian`, `ArtDeco`). Customers expect matching furniture — a Modern sofa shouldn't be paired with a Victorian chair.

**Solution**

1. Declare interfaces for each distinct product (`Chair`, `Sofa`, `CoffeeTable`).
2. Declare the **Abstract Factory** interface with creation methods for each product.
3. Create concrete factory classes for each variant (`ModernFactory`, `VictorianFactory`) that create only their variant's products.
4. Client code works only with the abstract factory/product interfaces.

---

**Structure**

1. **Abstract Products** — `Chair`, `Sofa`, `CoffeeTable` interfaces
2. **Concrete Products** — `ModernChair`, `VictorianChair`, etc.
3. **Abstract Factory** — declares `createChair()`, `createSofa()`, `createCoffeeTable()`
4. **Concrete Factories** — `ModernFactory`, `VictorianFactory` — implement the factory interface
5. **Client** — works via abstract interfaces only

---

**Pseudocode Example** (Cross-platform UI)

```pseudocode
interface GUIFactory
  method createButton(): Button
  method createCheckbox(): Checkbox

class WinFactory implements GUIFactory
  method createButton(): Button → return new WinButton()
  method createCheckbox(): Checkbox → return new WinCheckbox()

class MacFactory implements GUIFactory
  method createButton(): Button → return new MacButton()
  method createCheckbox(): Checkbox → return new MacCheckbox()

class Application
  constructor(factory: GUIFactory)
    this.button = factory.createButton()
  method paint()
    button.paint()
```

---

**Applicability**

- When code must work with various families of related products.
- When a class has a set of Factory Methods that blur its primary responsibility.

**Pros**
- Compatible products guaranteed.
- Avoids tight coupling between concrete products and client code.
- Single Responsibility; Open/Closed.

**Cons**
- More interfaces and classes — increased complexity.

**Relations**
- Often based on Factory Methods.
- Can serve as alternative to Facade.
- Works with Bridge for implementations that match specific abstractions.

---

### Builder

**Intent:** Lets you construct **complex objects step by step**. Produces different types and representations using the same construction code.

---

**Problem**

A `House` object with many optional fields (swimming pool, garden, fireplace, etc.). Either a giant constructor with many parameters (telescoping constructor) or a huge number of subclasses.

**Solution**

Extract object construction into a separate **builder** object. Construction happens via a series of steps (`buildWalls()`, `buildDoor()`, `buildRoof()`). You only call the steps you need.

**Director**: An optional class that defines the order of construction steps and can create several predefined product configurations.

---

**Structure**

1. **Builder interface** — declares common construction steps
2. **Concrete Builders** — implement the steps; may produce entirely different products
3. **Products** — the resulting objects (don't need a common interface)
4. **Director** — defines the order of construction steps
5. **Client** — associates a builder with a director; retrieves result from builder

---

**Pseudocode Example** (Car and Manual)

```pseudocode
interface Builder
  reset(), setSeats(), setEngine(), setTripComputer(), setGPS()

class CarBuilder implements Builder
  method getProduct(): Car

class CarManualBuilder implements Builder
  method getProduct(): Manual

class Director
  method constructSportsCar(builder: Builder)
    builder.reset()
    builder.setSeats(2)
    builder.setEngine(new SportEngine())
    builder.setGPS(true)
```

---

**Applicability**

- To eliminate "telescopic constructors" with many optional parameters.
- When you need different representations of the same product.
- To construct Composite trees or other complex objects step by step.

**How to Implement**

1. Define common construction steps that cover all product representations.
2. Declare these steps in the builder interface.
3. Create concrete builder classes for each product representation.
4. Optionally create a Director class.
5. Client creates builder, passes to director, gets result.

**Pros**
- Build step-by-step; defer or run steps recursively.
- Reuse same construction code for different representations.
- Single Responsibility: complex construction isolated from business logic.

**Cons**
- Overall complexity increases (more new classes).

**Relations**
- Works with Bridge (director = abstraction, builders = implementations).
- Can build Composite trees recursively.
- Abstract Factories, Builders, and Prototypes can be implemented as Singletons.

---

### Prototype

> Also known as: **Clone**

**Intent:** Lets you copy existing objects without making your code dependent on their classes.

---

**Problem**

You want to create an exact copy of an object, but some fields are private and inaccessible from outside. Also, you might not know the concrete class of the object — only its interface.

**Solution**

Delegate the cloning to the objects themselves. Declare a common `clone()` interface. The implementation copies all fields (including private ones, since objects of the same class can access each other's private members).

An object that supports cloning is called a **prototype**.

**Prototype Registry**: A centralized store of pre-built prototypes accessible by name or other criteria.

---

**Structure**

1. **Prototype interface** — declares `clone()` method
2. **Concrete Prototype** — implements `clone()`, handles edge cases (circular refs, etc.)
3. **Client** — can produce copies of any object following the prototype interface
4. (Optional) **Prototype Registry** — name → prototype map for frequently used objects

---

**Pseudocode Example**

```pseudocode
abstract class Shape
  constructor Shape(source: Shape)
    this.X = source.X; this.Y = source.Y; this.color = source.color
  abstract method clone(): Shape

class Rectangle extends Shape
  constructor Rectangle(source: Rectangle)
    super(source); this.width = source.width; this.height = source.height
  method clone(): Shape → return new Rectangle(this)

class Circle extends Shape
  method clone(): Shape → return new Circle(this)
```

---

**Applicability**

- When code shouldn't depend on concrete classes of objects being copied.
- To reduce subclasses that differ only in initialization.

**Pros**
- Clone without coupling to concrete classes.
- Replace repeated initialization with cloning pre-built prototypes.
- Alternative to inheritance for configuration presets.

**Cons**
- Cloning objects with circular references can be tricky.

**Relations**
- Can save copies of Commands into history.
- Useful with Composite and Decorator to clone complex structures.
- Sometimes a simpler alternative to Memento.

---

### Singleton

**Intent:** Ensures a class has **only one instance** while providing a **global access point** to it.

---

**Problem**

Two problems solved simultaneously (violating SRP):
1. Ensure a class has just one instance (e.g., shared database connection).
2. Provide a global access point to that instance.

**Why not just globals?** Globals can be overwritten. Singleton protects the instance.

**Solution**

- Make the **default constructor private**.
- Create a **static creation method** that calls the private constructor on first invocation and caches the result. All subsequent calls return the cached object.

---

**Structure**

1. **Singleton class** — has a private static instance field; declares static `getInstance()` method.

---

**Pseudocode Example**

```pseudocode
class Database
  private static field instance: Database
  private constructor Database() // initialization code

  public static method getInstance()
    if (this.instance == null)
      acquireThreadLock()
      if (this.instance == null)
        this.instance = new Database()
    return this.instance

  public method query(sql) // business logic
```

---

**Applicability**

- When exactly one instance should be accessible to all clients.
- When you need stricter control over global variables.

**How to Implement**

1. Add a private static field to store the instance.
2. Declare a public static creation method.
3. Implement lazy initialization in the static method.
4. Make the constructor private.
5. Replace all direct constructor calls in client code with the static method.

**Pros**
- Guaranteed single instance.
- Global access point.
- Lazy initialization.

**Cons**
- Violates Single Responsibility Principle.
- Can mask bad design.
- Requires special treatment in multi-threaded environments.
- Difficult to unit test (private constructor, no mock).

**Relations**
- Facade can be transformed into Singleton.
- Flyweight resembles Singleton but can have multiple instances with different states; Singleton is mutable, Flyweight objects are immutable.

---

## Structural Design Patterns

Structural patterns explain how to assemble objects and classes into larger structures while keeping them flexible and efficient.

---

### Adapter

> Also known as: **Wrapper**

**Intent:** Allows objects with **incompatible interfaces** to collaborate.

---

**Problem**

A stock market app downloads XML data. A third-party analytics library only accepts JSON. You can't modify the library.

**Solution**

Create an **adapter** — a special object that converts the interface of one object so another object can understand it. The adapter wraps one of the objects, hiding the conversion complexity. The wrapped object is unaware of the adapter.

---

**Structure**

**Object Adapter** (uses composition):

1. **Client** — existing business logic
2. **Client Interface** — protocol other classes must follow
3. **Service** — useful class with incompatible interface
4. **Adapter** — implements client interface, wraps the service, translates calls

**Class Adapter** (uses multiple inheritance, C++ only):
- Inherits from both client and service simultaneously.

---

**Pseudocode Example** (Square peg in round hole)

```pseudocode
class RoundHole
  method fits(peg: RoundPeg): bool

class SquarePegAdapter extends RoundPeg
  private field peg: SquarePeg
  constructor(peg: SquarePeg)
  method getRadius()
    return peg.getWidth() * Math.sqrt(2) / 2

// Usage
hole = new RoundHole(5)
small_sqpeg_adapter = new SquarePegAdapter(new SquarePeg(5))
hole.fits(small_sqpeg_adapter) // true
```

---

**Applicability**

- When you want to use an existing class but its interface isn't compatible.
- When you want to reuse several subclasses that lack some common functionality.

**Pros**
- Single Responsibility: interface/data conversion separated from business logic.
- Open/Closed: new adapters without breaking existing client code.

**Cons**
- Overall code complexity increases.

**Relations**
- Bridge is designed up-front; Adapter is used with existing apps.
- Adapter changes interface; Decorator enhances without changing interface.
- Facade defines a new interface; Adapter makes existing interface usable.
- Proxy provides the same interface; Decorator provides an enhanced interface.

---

### Bridge

**Intent:** Splits a large class or closely related classes into two separate hierarchies — **abstraction** and **implementation** — which can be developed independently.

---

**Problem**

A `Shape` class with `Circle` and `Square` subclasses. You want to add colors (Red, Blue). You'd need `BlueCircle`, `RedSquare`, etc. — an exponential growth in class combinations.

**Solution**

Extract one dimension (color) into a separate class hierarchy. `Shape` holds a **reference** to a `Color` object. Adding new colors doesn't require modifying Shape subclasses, and vice versa.

**Abstraction** = high-level control layer (GUI layer, remote control)  
**Implementation** = underlying layer that does the actual work (OS API, device)

---

**Structure**

1. **Abstraction** — high-level control logic; holds reference to implementation
2. **Implementation** (interface) — declares methods common to all implementations
3. **Concrete Implementations** — platform-specific code
4. **Refined Abstractions** — variants of control logic
5. **Client** — links an abstraction to an implementation

---

**Pseudocode Example** (Remote control + Device)

```pseudocode
class RemoteControl
  protected field device: Device
  method togglePower()
    if device.isEnabled() → device.disable() else device.enable()
  method volumeDown() → device.setVolume(device.getVolume() - 10)

class AdvancedRemoteControl extends RemoteControl
  method mute() → device.setVolume(0)

interface Device
  isEnabled(), enable(), disable(), getVolume(), setVolume(), getChannel(), setChannel()

class Tv implements Device // ...
class Radio implements Device // ...
```

---

**Applicability**

- To divide a monolithic class with several variants of some functionality.
- When you need to extend in several orthogonal (independent) dimensions.
- When you need to switch implementations at runtime.

**Pros**
- Platform-independent classes/apps.
- Open/Closed and Single Responsibility principles.
- High-level abstraction is isolated from platform details.

**Cons**
- Can make code more complicated when applied to a highly cohesive class.

**Relations**
- Abstract Factory can encapsulate Bridge relations and hide complexity.
- Builder + Bridge: director = abstraction, builders = implementations.

---

### Composite

> Also known as: **Object Tree**

**Intent:** Lets you compose objects into **tree structures** and then work with these structures as if they were individual objects.

---

**Problem**

An ordering system with `Products` and `Boxes`. A `Box` contains `Products` and smaller `Boxes`. How do you calculate the total price without knowing the depth of nesting?

**Solution**

Implement a common interface with a `getPrice()` method. For a `Product`, it returns its price. For a `Box`, it iterates over its contents and sums up prices recursively.

The greatest benefit: you don't care whether an object is a simple product or a complex box — treat them all the same via the common interface.

---

**Structure**

1. **Component interface** — operations common to both leaves and containers
2. **Leaf** — basic element with no sub-elements; does most actual work
3. **Container (Composite)** — has sub-elements; delegates work to children and aggregates results
4. **Client** — works with all elements through the component interface

---

**Pseudocode Example** (Graphic shapes editor)

```pseudocode
interface Graphic
  method move(x, y)
  method draw()

class Dot implements Graphic // leaf
class Circle extends Dot // leaf

class CompoundGraphic implements Graphic
  field children: array of Graphic
  method add(child), remove(child)
  method move(x, y) → foreach child: child.move(x, y)
  method draw() → foreach child: child.draw()
```

---

**Applicability**

- To implement a tree-like object structure.
- When you want client code to treat both simple and complex elements uniformly.

**Pros**
- Polymorphism and recursion advantage.
- Open/Closed: introduce new element types without breaking existing code.

**Cons**
- Hard to provide a common interface for classes whose functionality differs too much.

**Relations**
- Use Builder to construct complex Composite trees.
- Chain of Responsibility often used with Composite.
- Iterators traverse Composite trees.
- Flyweight for shared leaf nodes.
- Composite and Decorator have similar structures but different purposes.

---

### Decorator

> Also known as: **Wrapper**

**Intent:** Lets you attach new behaviors to objects by placing them inside **special wrapper objects** that contain the behaviors.

---

**Problem**

A notification library that only sends emails. Users want SMS, Facebook, Slack notifications. Creating subclasses for every combination explodes the hierarchy.

**Solution**

Use composition over inheritance. A **wrapper** has the same interface as the target. The wrapper receives calls, may add behavior before/after, then delegates to the wrapped object.

Stack decorators — each adds its own behavior, client sees a single object with combined behavior.

> Like wearing clothes: a sweater, then a jacket, then a raincoat — each "extends" your basic behavior.

---

**Structure**

1. **Component interface** — common interface for wrappers and wrapped objects
2. **Concrete Component** — base object with basic behavior
3. **Base Decorator** — wraps a component object; delegates all work to it
4. **Concrete Decorators** — override methods to add behavior before/after calling the parent
5. **Client** — wraps components in multiple layers of decorators

---

**Pseudocode Example** (Encryption + Compression)

```pseudocode
interface DataSource
  method writeData(data), readData(): data

class FileDataSource implements DataSource // base

class DataSourceDecorator implements DataSource
  protected field wrappee: DataSource
  method writeData(data) → wrappee.writeData(data)

class EncryptionDecorator extends DataSourceDecorator
  method writeData(data)
    // 1. Encrypt data
    // 2. wrappee.writeData(encryptedData)

class CompressionDecorator extends DataSourceDecorator
  method writeData(data)
    // 1. Compress data
    // 2. wrappee.writeData(compressedData)

// Usage
source = new FileDataSource("file.dat")
source = new CompressionDecorator(source)
source = new EncryptionDecorator(source)
source.writeData(data) // writes encrypted & compressed data
```

---

**Applicability**

- When you need to assign extra behaviors to objects at runtime without breaking existing code.
- When it's awkward or impossible to extend behavior using inheritance (e.g., `final` class).

**Pros**
- Extend behavior without subclassing.
- Add/remove responsibilities at runtime.
- Combine several behaviors via multiple decorators.
- Single Responsibility.

**Cons**
- Hard to remove a specific wrapper.
- Order in the decorator stack matters.
- Initial configuration code may look ugly.

**Relations**
- Adapter changes interface; Decorator enhances without changing it.
- Decorator supports recursive composition; Proxy does not.
- Chain of Responsibility vs. Decorator: CoR handlers can stop the chain; decorators can't.

---

### Facade

**Intent:** Provides a **simplified interface** to a library, framework, or any complex set of classes.

---

**Problem**

Working with a complex library requires initializing many objects, tracking dependencies, and executing methods in the correct order — creating tight coupling to the library.

**Solution**

Create a **Facade** class that provides a simple interface to the complex subsystem. It limits the available functionality but includes only what clients care about.

> Like a phone operator in a shop — a single voice interface to the ordering system, payment gateways, and delivery services.

---

**Structure**

1. **Facade** — knows where to direct requests and how to operate the subsystem
2. **Additional Facades** — can be created for different subsystem features
3. **Complex Subsystem** — dozens of objects doing actual work; unaware of the facade
4. **Client** — uses the facade instead of calling subsystem directly

---

**Pseudocode Example** (Video Conversion)

```pseudocode
class VideoConverter
  method convert(filename, format): File
    file = new VideoFile(filename)
    sourceCodec = CodecFactory.extract(file)
    destinationCodec = format == "mp4" ? MPEG4CompressionCodec() : OggCompressionCodec()
    buffer = BitrateReader.read(filename, sourceCodec)
    result = BitrateReader.convert(buffer, destinationCodec)
    result = (new AudioMixer()).fix(result)
    return new File(result)

// Client only uses the Facade
convertor = new VideoConverter()
mp4 = convertor.convert("video.ogg", "mp4")
```

---

**Applicability**

- When you need a limited but straightforward interface to a complex subsystem.
- When you want to layer a subsystem, defining entry points to each level.

**Pros**
- Isolate code from subsystem complexity.

**Cons**
- A facade can become a **God object** coupled to all classes.

**Relations**
- Facade defines new interface; Adapter makes existing interface usable.
- Facade can serve as a Singleton.
- Facade shows how to make one object represent an entire subsystem; Flyweight shows many small objects.
- Facade and Mediator: Facade defines a simplified interface; Mediator centralizes communication between components.

---

### Flyweight

> Also known as: **Cache**

**Intent:** Lets you fit more objects into available RAM by **sharing common parts** of state between multiple objects instead of keeping all data in each object.

---

**Problem**

A video game with a particle system. Each particle (bullet, missile, shrapnel) stores color, sprite, position, velocity, speed. The game crashes because memory is exhausted.

**Solution**

Notice that `color` and `sprite` are shared between many particles of the same type. Move this **intrinsic state** (constant, shared) into a **Flyweight** object. Leave the **extrinsic state** (variable, context-specific: position, velocity) in the context object.

- **Intrinsic state** — lives within the flyweight object; immutable; shared
- **Extrinsic state** — passed to flyweight methods as parameters; unique per instance

**Flyweight Factory**: manages a pool of existing flyweights, creating new ones only when needed.

---

**Structure**

1. **Flyweight class** — stores intrinsic state; immutable (no setters)
2. **Context class** — stores extrinsic state; references a flyweight
3. **Flyweight Factory** — manages the pool; returns existing flyweight or creates new one
4. **Client** — stores extrinsic state; calls flyweight methods passing extrinsic state as args

---

**Pseudocode Example** (Forest of trees)

```pseudocode
class TreeType // flyweight: name, color, texture
  method draw(canvas, x, y) // draws tree at (x,y)

class TreeFactory
  static field treeTypes: collection
  static method getTreeType(name, color, texture)
    type = treeTypes.find(name, color, texture)
    if type == null → type = new TreeType(...); treeTypes.add(type)
    return type

class Tree // context: x, y, type: TreeType
  method draw(canvas) → type.draw(canvas, x, y)

class Forest
  method plantTree(x, y, name, color, texture)
    type = TreeFactory.getTreeType(name, color, texture)
    tree = new Tree(x, y, type)
    trees.add(tree)
```

---

**Applicability**

Only when your program must support a huge number of objects that barely fit in RAM, and those objects contain duplicated state that can be extracted and shared.

**Pros**
- Huge RAM savings when many similar objects exist.

**Cons**
- Trade RAM for CPU (extrinsic state recalculated each call).
- Code becomes more complicated.

**Relations**
- Flyweight + Composite: implement shared leaf nodes as Flyweights.
- Flyweight resembles Singleton but can have multiple instances with different intrinsic states.

---

### Proxy

**Intent:** Provides a **substitute or placeholder** for another object to control access to it, allowing something to be performed before or after the request reaches the original.

---

**Problem**

A massive object (database connection) consumes resources. You want lazy initialization — create it only when needed. But the logic for that would be duplicated everywhere.

**Solution**

Create a proxy class with the same interface as the original. The proxy creates the real object when needed and delegates all work to it. The proxy can also add behavior (caching, logging, access control).

> Like a credit card (proxy) for a bank account (proxy for cash). Both implement the "payment" interface.

---

**Structure**

1. **Service Interface** — proxy must follow this interface
2. **Service** — actual business logic
3. **Proxy** — holds a reference to service; handles pre/post processing; manages lifecycle
4. **Client** — works with both service and proxy via same interface

---

**Pseudocode Example** (YouTube caching proxy)

```pseudocode
interface ThirdPartyYoutubeLib
  listVideos(), getVideoInfo(id), downloadVideo(id)

class ThirdPartyYoutubeClass implements ThirdPartyYoutubeLib // real service

class CachedYoutubeClass implements ThirdPartyYoutubeLib
  private service, listCache, videoCache
  method listVideos()
    if listCache == null → listCache = service.listVideos()
    return listCache
  method downloadVideo(id)
    if !downloadExists(id) → service.downloadVideo(id)
```

---

**Use Cases**

- **Lazy initialization** (virtual proxy) — delay creation of heavyweight object
- **Access control** (protection proxy) — only allow specific clients
- **Remote proxy** — handle network communication for remote service
- **Logging proxy** — log each request
- **Caching proxy** — cache results of recurring requests
- **Smart reference** — dismiss heavyweight object when no clients use it

**How to Implement**

1. Create proxy class (or make it a subclass of service if no interface exists).
2. Add a field for storing a reference to the service.
3. Implement proxy methods; delegate most work to service.
4. Consider introducing a factory method to decide client gets proxy or real service.
5. Implement lazy initialization if needed.

**Pros**
- Control service object without clients knowing.
- Manage service object lifecycle.
- Proxy works even if service is unavailable.
- Open/Closed: introduce new proxies without changing service.

**Cons**
- More classes; response may be delayed.

**Relations**
- Adapter: different interface. Proxy: same interface. Decorator: enhanced interface.
- Proxy manages service lifecycle; Decorator composition is client-controlled.

---

## Behavioral Design Patterns

Behavioral patterns take care of effective communication and assignment of responsibilities between objects.

---

### Chain of Responsibility

> Also known as: **CoR, Chain of Command**

**Intent:** Lets you pass requests along a **chain of handlers**. Each handler decides either to process the request or pass it to the next handler.

---

**Problem**

An ordering system with multiple sequential checks: authentication, data validation, rate limiting, caching. Each check became tightly coupled to the others. Adding or removing checks requires modifying the entire chain.

**Solution**

Transform each check into a standalone **handler** object. Link handlers into a chain. Each handler:
1. Decides if it can handle the request.
2. Either processes it and stops, or passes it to the next handler.

---

**Structure**

1. **Handler interface** — declares `handle(request)` and optionally `setNext(handler)`
2. **Base Handler** (optional) — stores next handler reference; default behavior: forwards to next
3. **Concrete Handlers** — actual processing logic; decides to process or pass
4. **Client** — composes the chain; can send to any handler in the chain

---

**Pseudocode Example** (GUI contextual help)

```pseudocode
abstract class Component implements ComponentWithContextualHelp
  protected field container: Container
  method showHelp()
    if tooltipText != null → show tooltip
    else → container.showHelp()

class Panel extends Container
  method showHelp()
    if modalHelpText != null → show modal
    else → super.showHelp()

class Dialog extends Container
  method showHelp()
    if wikiPageURL != null → open wiki
    else → super.showHelp()
```

---

**Applicability**

- When you need to process different kinds of requests in various ways and the sequence is unknown.
- When handlers must execute in a particular order.
- When the set of handlers and their order should change at runtime.

**Pros**
- Control the order of request handling.
- Single Responsibility: decouple invokers from performers.
- Open/Closed: introduce new handlers without breaking existing code.

**Cons**
- Some requests may go unhandled.

**Relations**
- CoR, Command, Mediator, Observer address connecting senders and receivers differently.
- Often used with Composite (leaf passes request up through parent chain).

---

### Command

> Also known as: **Action, Transaction**

**Intent:** Turns a request into a **stand-alone object** containing all information about the request. Enables parameterized methods, delayed/queued execution, and undoable operations.

---

**Problem**

A text editor toolbar with Copy, Cut, Paste buttons. These buttons share code with keyboard shortcuts and context menus. Tight coupling between GUI and business logic. Duplicate code everywhere.

**Solution**

Extract all request details into a **Command** object with a single `execute()` method. GUI objects trigger commands; commands handle details and delegate to receivers (business logic objects).

> Like a waiter writing your order on paper — the order is the command, it sits in queue, and the chef executes it.

---

**Structure**

1. **Sender (Invoker)** — triggers the command; stores command reference; doesn't know what the command does
2. **Command interface** — declares `execute()`
3. **Concrete Commands** — delegates work to receiver; parameters stored as fields
4. **Receiver** — actual business logic (editor, document, etc.)
5. **Client** — creates commands, associates with senders and receivers

---

**Pseudocode Example** (Text editor undo/redo)

```pseudocode
abstract class Command
  protected field app, editor, backup
  method saveBackup() → backup = editor.text
  method undo() → editor.text = backup
  abstract method execute()

class CopyCommand extends Command
  method execute() → app.clipboard = editor.getSelection(); return false

class CutCommand extends Command
  method execute() → saveBackup(); app.clipboard = editor.getSelection(); editor.deleteSelection(); return true

class CommandHistory
  field history: array of Command
  method push(c), pop(): Command

class Application
  method executeCommand(command)
    if command.execute() → history.push(command)
  method undo()
    command = history.pop()
    if command != null → command.undo()
```

---

**Applicability**

- To parameterize objects with operations.
- To queue, schedule, or execute operations remotely.
- To implement reversible (undo/redo) operations.

**Pros**
- Single Responsibility; Open/Closed.
- Implement undo/redo.
- Deferred execution.
- Compose complex commands from simple ones.

**Cons**
- New layer between senders and receivers increases complexity.

**Relations**
- Command + Memento for undo (commands perform operations; mementos save state).
- Prototype can save copies of Commands in history.
- Visitor is a powerful version of Command (can execute on various object types).

---

### Iterator

**Intent:** Lets you traverse elements of a **collection** without exposing its underlying representation.

---

**Problem**

Collections come in many forms (lists, stacks, trees, graphs). Clients shouldn't care about the internal structure. But different structures need different traversal algorithms (depth-first, breadth-first, random access).

**Solution**

Extract traversal behavior into a separate **iterator** object. The iterator encapsulates: current position, how many elements remain, the algorithm itself. Multiple iterators can traverse the same collection independently.

---

**Structure**

1. **Iterator interface** — `getNext()`, `hasMore()`, optionally `getPrev()`, `reset()`
2. **Concrete Iterators** — implement specific traversal algorithms
3. **Collection interface** — declares `createIterator()` factory method
4. **Concrete Collections** — return specific iterator instances
5. **Client** — works with collections and iterators via interfaces only

---

**Pseudocode Example** (Social network profiles)

```pseudocode
interface SocialNetwork
  createFriendsIterator(profileId): ProfileIterator
  createCoworkersIterator(profileId): ProfileIterator

class Facebook implements SocialNetwork
  method createFriendsIterator(profileId)
    return new FacebookIterator(this, profileId, "friends")

interface ProfileIterator
  getNext(): Profile, hasMore(): bool

class SocialSpammer
  method send(iterator: ProfileIterator, message)
    while iterator.hasNext()
      profile = iterator.getNext()
      system.sendEmail(profile.getEmail(), message)
```

---

**Applicability**

- When a collection has a complex data structure but you want to hide complexity.
- To reduce duplicate traversal code across the app.
- When you want code to traverse different data structures.

**Pros**
- Single Responsibility; Open/Closed.
- Parallel iteration with independent state per iterator.
- Delay iteration and continue when needed.

**Cons**
- Overkill for simple collections.
- May be less efficient than direct element access in specialized collections.

**Relations**
- Factory Method + Iterator for collection subclasses to return different iterators.
- Memento + Iterator to capture and restore iteration state.
- Visitor + Iterator to traverse and operate over complex structures.

---

### Mediator

> Also known as: **Intermediary, Controller**

**Intent:** Reduces chaotic dependencies between objects. Forces them to communicate **only via a mediator object**.

---

**Problem**

A customer profile editing form. The "submit" button must validate many fields. Selecting a checkbox reveals a hidden text field. All these dependencies are hard-coded into form elements, making them impossible to reuse.

**Solution**

All direct communication between components ceases. Components notify a **Mediator** object about events. The mediator decides what to do and redirects calls to the appropriate components.

> Like an air traffic controller — pilots don't communicate with each other directly; all communication goes through the control tower.

---

**Structure**

1. **Components** — business logic classes; each has a mediator reference; unaware of other components
2. **Mediator interface** — declares `notify(sender, event)`
3. **Concrete Mediators** — encapsulate relations; keep references to all managed components
4. **Client** — creates mediator and all components; links them together

---

**Pseudocode Example** (Authentication dialog)

```pseudocode
interface Mediator
  method notify(sender: Component, event: string)

class AuthenticationDialog implements Mediator
  method notify(sender, event)
    if sender == loginChkBx and event == "check" →
      if checked → show login form, hide register form
      else → show register form, hide login form
    if sender == okBtn and event == "click" →
      validate credentials or create account

class Component
  field dialog: Mediator
  method click() → dialog.notify(this, "click")
  method keypress() → dialog.notify(this, "keypress")
```

---

**Applicability**

- When it's hard to change classes because of tight coupling with many others.
- When you can't reuse a component in a different program due to dependencies.
- When you're creating tons of component subclasses just to reuse basic behavior.

**Pros**
- Single Responsibility; Open/Closed.
- Reduce coupling between program components.
- Easier to reuse individual components.

**Cons**
- Over time, a Mediator can evolve into a **God Object**.

**Relations**
- Facade and Mediator: Facade = simplified interface, subsystem components communicate directly. Mediator = centralized communication, components only talk to mediator.
- Mediator vs. Observer: Mediator eliminates mutual dependencies; Observer establishes dynamic one-way connections.

---

### Memento

> Also known as: **Snapshot**

**Intent:** Lets you save and restore the previous state of an object **without revealing the details of its implementation**.

---

**Problem**

A text editor needs undo functionality. Naive approach: copy all fields to a storage object. But many fields are private. Making them public breaks encapsulation. Changes to the class would ripple to all snapshot code.

**Solution**

The **originator** (object whose state we save) creates its own snapshots. The snapshot (memento) is only accessible to the originator. A **caretaker** stores mementos but can only work with their limited interface (metadata only).

---

**Structure (nested classes)**

1. **Originator** — creates snapshots of own state; can restore from snapshot
2. **Memento (Snapshot)** — immutable value object; only originator can access its full contents
3. **Caretaker** — stores stack of mementos; passes them back for restoration

**Alternate implementation** (no nested classes): Use an intermediary interface for caretakers; originators work directly with the memento class.

---

**Pseudocode Example**

```pseudocode
class Editor // originator
  private field text, curX, curY, selectionWidth
  method createSnapshot(): Snapshot
    return new Snapshot(this, text, curX, curY, selectionWidth)

class Snapshot // memento
  private editor, text, curX, curY, selectionWidth
  method restore()
    editor.setText(text)
    editor.setCursor(curX, curY)
    editor.setSelectionWidth(selectionWidth)

class Command // caretaker role
  private backup: Snapshot
  method makeBackup() → backup = editor.createSnapshot()
  method undo() → if backup != null → backup.restore()
```

---

**Applicability**

- To produce snapshots of an object's state for undo/rollback.
- When direct access to an object's fields violates its encapsulation.

**Pros**
- Produce state snapshots without violating encapsulation.
- Simplify originator's code (caretaker maintains history).

**Cons**
- High RAM usage if mementos are created too often.
- Caretakers must track originator lifecycle to destroy obsolete mementos.
- Dynamic languages (PHP, Python, JS) can't guarantee memento state immutability.

**Relations**
- Command + Memento for undo (commands perform operations; mementos save state).
- Memento + Iterator to capture/restore iteration state.
- Prototype can be a simpler alternative to Memento for straightforward objects.

---

### Observer

> Also known as: **Event-Subscriber, Listener**

**Intent:** Defines a **subscription mechanism** to notify multiple objects about events happening to the observed object.

---

**Problem**

A `Customer` wants to know when an `iPhone` becomes available at a `Store`. The customer could check every day (wasteful). The store could email all customers (spam). Neither is ideal.

**Solution**

The observed object (**publisher/subject**) maintains a **subscription list** of **subscribers**. It notifies all subscribers when an important event occurs. Subscribers can subscribe/unsubscribe dynamically.

> Like a newspaper subscription — you receive each issue automatically instead of checking the store.

---

**Structure**

1. **Publisher** — maintains subscription list; provides subscribe/unsubscribe methods; notifies subscribers
2. **Subscriber interface** — declares `update(data)` notification method
3. **Concrete Subscribers** — react to notifications (logging, email alerts, etc.)
4. **Client** — creates publishers and subscribers; registers subscribers

---

**Pseudocode Example** (Text editor events)

```pseudocode
class EventManager
  private field listeners: hash map of (eventType → listeners)
  method subscribe(eventType, listener)
  method unsubscribe(eventType, listener)
  method notify(eventType, data)
    foreach listener in listeners[eventType] → listener.update(data)

class Editor
  private events: EventManager
  method openFile(path) → events.notify("open", file.name)
  method saveFile() → events.notify("save", file.name)

class LoggingListener implements EventListener
  method update(filename) → log.write(message.replace('%s', filename))

class EmailAlertsListener implements EventListener
  method update(filename) → system.email(email, message.replace('%s', filename))
```

---

**Applicability**

- When changes to one object's state may require changing others, but the set of objects is unknown or changes dynamically.
- When some objects must observe others, but only for a limited time or in specific cases.

**Pros**
- Open/Closed: introduce new subscriber classes without changing publisher.
- Establish object relations at runtime.

**Cons**
- Subscribers are notified in random order.

**Relations**
- Mediator vs. Observer: Mediator eliminates mutual dependencies (components → mediator). Observer establishes dynamic one-way connections.

---

### State

**Intent:** Lets an object **alter its behavior when its internal state changes**. It appears as if the object changed its class.

---

**Problem**

A `Document` can be in `Draft`, `Moderation`, or `Published` state. The `publish()` method behaves differently in each state. Implemented with conditionals, the code becomes a mess as states grow.

**Solution**

Create separate classes for each state. The original **context** object stores a reference to the current state object and delegates all state-specific work to it. To change state, replace the state object.

Key difference from Strategy: **States may be aware of each other** and can initiate transitions between states. Strategies are independent and don't know about each other.

---

**Structure**

1. **Context** — stores reference to current state object; delegates state-specific work
2. **State interface** — declares state-specific methods
3. **Concrete States** — implement state-specific methods; may hold a backreference to context for transitions
4. Both context and concrete states can set the next state

---

**Pseudocode Example** (Audio player)

```pseudocode
class AudioPlayer // context
  field state: State
  method changeState(state: State) → this.state = state
  method clickLock() → state.clickLock()
  method clickPlay() → state.clickPlay()

abstract class State
  protected field player: AudioPlayer
  abstract clickLock(), clickPlay(), clickNext(), clickPrevious()

class LockedState extends State
  method clickLock()
    if player.playing → player.changeState(new PlayingState(player))
    else → player.changeState(new ReadyState(player))

class ReadyState extends State
  method clickPlay()
    player.startPlayback()
    player.changeState(new PlayingState(player))

class PlayingState extends State
  method clickPlay()
    player.stopPlayback()
    player.changeState(new ReadyState(player))
```

---

**Applicability**

- When an object behaves differently depending on its state, many states exist, and state-specific code changes frequently.
- When a class is polluted with massive conditionals that alter behavior based on field values.
- When duplicate code exists across similar states and transitions.

**Pros**
- Single Responsibility; Open/Closed.
- Eliminate bulky state machine conditionals.

**Cons**
- Overkill if only a few states exist or they rarely change.

**Relations**
- Bridge, State, Strategy (and Adapter) have similar structures based on composition.
- State is an extension of Strategy — but State allows states to know about each other.

---

### Strategy

**Intent:** Defines a family of algorithms, puts each in a separate class, and makes their objects **interchangeable**.

---

**Problem**

A navigation app with route planning. Initially only road routes. Then walking, public transport, cycling, tourist attractions. The main class doubled in size with each new algorithm, becoming hard to maintain.

**Solution**

Extract all routing algorithms into separate **strategy** classes, all implementing the same interface. The **context** (navigator) stores a reference to a strategy and delegates work to it. The client can switch strategies at runtime.

---

**Structure**

1. **Context** — maintains reference to a concrete strategy; exposes a setter to change it
2. **Strategy interface** — `execute(a, b)` method common to all strategies
3. **Concrete Strategies** — different algorithm implementations
4. **Client** — creates strategy object and passes to context

---

**Pseudocode Example** (Arithmetic operations)

```pseudocode
interface Strategy
  method execute(a, b)

class ConcreteStrategyAdd implements Strategy
  method execute(a, b) → return a + b

class ConcreteStrategySubtract implements Strategy
  method execute(a, b) → return a - b

class Context
  private strategy: Strategy
  method setStrategy(Strategy s) → this.strategy = s
  method executeStrategy(a, b) → return strategy.execute(a, b)
```

---

**Applicability**

- To use different algorithm variants within an object and switch at runtime.
- When many similar classes differ only in behavior.
- To isolate business logic from algorithm implementation details.
- When a class has a massive conditional switching between algorithm variants.

**Pros**
- Swap algorithms at runtime.
- Isolate implementation details.
- Replace inheritance with composition.
- Open/Closed.

**Cons**
- Overkill if only a couple of algorithms that rarely change.
- Clients must know about strategy differences.
- Modern functional languages can use lambda functions instead of strategy classes.

**Relations**
- Template Method (inheritance, static) vs. Strategy (composition, runtime).
- State is an extension of Strategy — states can know about each other.
- Decorator changes the skin; Strategy changes the guts.

---

### Template Method

**Intent:** Defines the **skeleton of an algorithm** in a superclass but lets subclasses override specific steps without changing the algorithm's structure.

---

**Problem**

A data mining app analyzes documents in DOC, CSV, PDF formats. All three classes share almost identical data processing and analysis code but differ in file reading. Duplicate code everywhere.

**Solution**

Break the algorithm into a series of steps, turn each into a method, and define the order in a **template method** in the base class. Steps may be abstract (must be overridden) or have default implementations. There are also **hooks** — optional empty methods before/after crucial steps.

---

**Structure**

1. **Abstract Class** — declares template method + abstract step methods; may provide default implementations for optional steps
2. **Concrete Classes** — implement abstract steps; may override optional steps; never override the template method itself

---

**Pseudocode Example** (Game AI)

```pseudocode
class GameAI
  method turn() // template method
    collectResources()
    buildStructures()
    buildUnits()
    attack()

  method collectResources() // default implementation
    foreach structure in builtStructures → structure.collect()

  abstract method buildStructures()
  abstract method buildUnits()
  method attack()
    enemy = closestEnemy()
    if enemy == null → sendScouts(map.center)
    else → sendWarriors(enemy.position)
  abstract method sendScouts(position)
  abstract method sendWarriors(position)

class OrcsAI extends GameAI
  method buildStructures() // orc-specific logic
  method buildUnits() // orc-specific logic
  method sendScouts(position) // orc-specific logic
  method sendWarriors(position) // orc-specific logic

class MonstersAI extends GameAI
  method collectResources() // do nothing
  method buildStructures() // do nothing
  method buildUnits() // do nothing
```

---

**Applicability**

- To let clients extend only particular steps of an algorithm, not the whole structure.
- When several classes contain almost identical algorithms with minor differences.

**Pros**
- Clients override only certain algorithm parts.
- Pull duplicate code into a superclass.

**Cons**
- Limited by provided skeleton.
- May violate Liskov Substitution Principle.
- Harder to maintain as the number of steps increases.

**Relations**
- Factory Method is a specialization of Template Method.
- Template Method (inheritance, static class-level) vs. Strategy (composition, object-level runtime).

---

### Visitor

**Intent:** Lets you **separate algorithms from the objects** on which they operate.

---

**Problem**

A graph of geographic nodes (cities, industries, sightseeing areas). You need to export it to XML. The architect refuses to let you add an export method to node classes (already in production). Future export formats are also anticipated.

**Solution**

Place the new behavior in a separate **visitor** class. The original object is passed to the visitor's method as an argument. The visitor implements separate methods for each node type.

**Double Dispatch**: Each element has an `accept(visitor)` method that calls the appropriate visitor method (`v.visitCity(this)`). This avoids the need for conditionals to check the object's type.

---

**Structure**

1. **Visitor interface** — declares `visit` methods for each concrete element class
2. **Concrete Visitors** — implement behaviors for each element type
3. **Element interface** — declares `accept(visitor)` method
4. **Concrete Elements** — implement `accept()` by calling the matching visitor method
5. **Client** — usually a collection/composite; passes visitor to elements

---

**Pseudocode Example** (XML export for geometric shapes)

```pseudocode
interface Shape
  method move(x, y), draw(), accept(v: Visitor)

class Dot extends Shape
  method accept(v: Visitor) → v.visitDot(this)

class Circle extends Dot
  method accept(v: Visitor) → v.visitCircle(this)

class Rectangle extends Shape
  method accept(v: Visitor) → v.visitRectangle(this)

interface Visitor
  visitDot(d), visitCircle(c), visitRectangle(r), visitCompoundShape(cs)

class XMLExportVisitor implements Visitor
  method visitDot(d) // export dot's ID and center coords
  method visitCircle(c) // export circle's ID, center, radius
  method visitRectangle(r) // export rectangle's ID, coords, width, height

// Client
exportVisitor = new XMLExportVisitor()
foreach shape in allShapes → shape.accept(exportVisitor)
```

---

**Applicability**

- When you need to perform operations on all elements of a complex object structure.
- To clean up business logic by extracting auxiliary behaviors into visitor classes.
- When a behavior makes sense only in some classes of a hierarchy.

**Pros**
- Open/Closed: introduce new behaviors without changing element classes.
- Single Responsibility: move related behaviors into one visitor class.
- Visitor can accumulate useful information while traversing.

**Cons**
- Must update all visitors when an element class is added/removed.
- Visitors may lack access to private fields/methods of elements.

**Relations**
- Visitor is a powerful version of Command (can execute on various object types).
- Visitor + Composite: execute operation over entire Composite tree.
- Visitor + Iterator: traverse complex structure and execute operations.

---

## Pattern Quick Reference

### Creational Patterns

| Pattern | Intent | Key Concept |
|---|---|---|
| **Factory Method** | Interface for creating objects; subclasses decide the type | Virtual Constructor |
| **Abstract Factory** | Create families of related objects | Product families |
| **Builder** | Construct complex objects step by step | Director + Builder |
| **Prototype** | Copy existing objects without depending on their class | `clone()` method |
| **Singleton** | Ensure only one instance with global access | Private constructor + static `getInstance()` |

### Structural Patterns

| Pattern | Intent | Key Concept |
|---|---|---|
| **Adapter** | Make incompatible interfaces work together | Wrapper that translates |
| **Bridge** | Separate abstraction from implementation | Two independent hierarchies |
| **Composite** | Compose objects into tree structures | Leaf + Container, same interface |
| **Decorator** | Add behavior by wrapping in objects | Wrapper with same interface + added behavior |
| **Facade** | Simplified interface to a complex subsystem | Single entry point |
| **Flyweight** | Share common state to reduce RAM usage | Intrinsic vs. extrinsic state |
| **Proxy** | Placeholder to control access to another object | Same interface, added control |

### Behavioral Patterns

| Pattern | Intent | Key Concept |
|---|---|---|
| **Chain of Responsibility** | Pass requests along a chain of handlers | Each handler processes or passes |
| **Command** | Encapsulate a request as an object | `execute()` + `undo()` |
| **Iterator** | Traverse a collection without exposing its structure | `getNext()`, `hasMore()` |
| **Mediator** | Centralize communication between objects | All through mediator |
| **Memento** | Save/restore object state without breaking encapsulation | Originator + Caretaker + Memento |
| **Observer** | Subscribe to events of another object | Publisher + Subscriber |
| **State** | Change behavior when internal state changes | State objects, context delegates |
| **Strategy** | Define interchangeable algorithms | Context holds strategy; swap at runtime |
| **Template Method** | Define algorithm skeleton in base class | Abstract steps; fixed structure |
| **Visitor** | Separate algorithm from object structure | Double dispatch, `accept(visitor)` |

---

## Pattern Relationships

```
Factory Method → evolves to → Abstract Factory / Builder / Prototype
Abstract Factory ←→ Builder (create families vs. step-by-step)
Prototype ←→ Memento (simpler alternative for state snapshots)
Singleton ←→ Facade (can transform Facade into Singleton)
Singleton ←→ Flyweight (related but different: mutability & count)

Adapter ←→ Bridge (similar structure; Adapter retrofits, Bridge is upfront)
Adapter ←→ Decorator ←→ Proxy (all wrap objects; differ by interface changes)
Composite ←→ Iterator (iterators traverse composite trees)
Composite ←→ Visitor (visitors execute over composite trees)
Composite + Decorator → Prototype (clone complex structures)
Decorator ←→ Strategy (skin vs. guts)
Facade ←→ Mediator (simplify communication; Facade = simplified API, Mediator = centralized hub)

CoR / Command / Mediator / Observer (four ways to connect senders & receivers)
Command + Memento → undo/redo
Iterator + Memento → save/restore iteration state
Iterator + Visitor → traverse & operate
State ← extends → Strategy
Template Method ← specialization → Factory Method
Visitor ← powerful version → Command
```

---

## Conclusion

Design patterns are a toolkit of tried-and-tested solutions to common problems in software design. The 22 GoF patterns covered in this document represent the foundation of object-oriented design vocabulary.

**Next steps:**

- Study code samples in specific programming languages.
- Read Joshua Kerievsky's *Refactoring to Patterns*.
- Apply patterns to real codebases through refactoring rather than building upfront.
- Remember: patterns are a guide — use them pragmatically, not dogmatically.

> *"Striving for these principles is good, but always try to be pragmatic and don't take everything as dogma."* — Alexander Shvets

---

*Based on: Dive Into Design Patterns by Alexander Shvets, Refactoring.Guru, 2019*
