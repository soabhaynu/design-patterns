# Design Patterns (GoF) - Notes + Implementations

This repo is for learning and building practical implementations of the **Gang of Four (GoF)** design patterns.

## What is a design pattern?
A **design pattern** is a reusable solution to a recurring design problem you run into while designing software. It doesn’t provide working code by itself; instead it describes **a proven structure, roles, and trade-offs** so you can implement the idea in your own codebase.

If you’ve used the same kind of structure in multiple projects (for example: “one shared instance”, “wrap behavior without changing callers”, “select an algorithm at runtime”), that’s usually a pattern in disguise.

## Why learn design patterns?
For an experienced engineer, patterns are useful because they:
1. Speed up design by reusing “known good” structures.
2. Improve communication (pattern names act like shorthand in reviews).
3. Make trade-offs explicit (flexibility vs complexity, coupling vs performance).
4. Provide a vocabulary for refactoring messy object creation / dependency flows.

## Types of GoF design patterns
GoF groups patterns into three categories:

- **[Creational](#creational-patterns)**: how objects are created (avoid duplicated `new` logic, centralize construction, control lifecycles).
- **[Structural](#structural-patterns)**: how classes/objects are composed (compose behavior, add wrappers, control access).
- **[Behavioral](#behavioral-patterns)**: how responsibilities and communication flow between objects (algorithms, events, state transitions).

## Important GoF patterns (practical for real-world engineering)
Below are the patterns that matter most often in long-lived systems. In each section, focus on: *intent*, *when to use*, and *the key structure*.

### Creational patterns
<a id="creational-patterns"></a>

#### 1) [Singleton](src/main/java/com/soabhaynu/design/creational/singleton/Singleton.md)
**Intent:** Ensure a class has only one instance and provide a global access point to it.  
**Use when:** You need exactly one shared resource (configuration, registry, logging facade, connection/session manager).  
**Key idea:** Control instantiation + control access (and handle thread-safety).

**References (read more):**
- [Wikipedia: Singleton pattern](https://en.wikipedia.org/wiki/Singleton_pattern)

#### 2) [Builder](src/main/java/com/soabhaynu/design/creational/builder/Builder.md)
**Intent:** Construct a complex object step-by-step while separating construction from representation.  
**Use when:** An object requires many optional parameters, or construction code becomes hard to read/maintain.  
**Key idea:** A `Builder` produces the `Product`; a `Director` (optional) controls the construction steps.

**References (read more):**
- [Wikipedia: Builder pattern](https://en.wikipedia.org/wiki/Builder_pattern)

#### 3) Factory Method
**Intent:** Define an interface for creating objects, but let subclasses decide which class to instantiate.  
**Use when:** You want polymorphism in creation without sprinkling `if/else` everywhere.  
**Key idea:** Creation is deferred to subclasses (or overridden factories).

**References (read more):**
- [Wikipedia: Factory method pattern](https://en.wikipedia.org/wiki/Factory_method_pattern)

#### 4) Abstract Factory
**Intent:** Create families of related objects without specifying their concrete classes.  
**Use when:** You must support multiple “platforms” or “variants” (UI kits, different database backends, theming).  
**Key idea:** A factory produces a consistent set of products.

#### 5) [Prototype](src/main/java/com/soabhaynu/design/creational/prototype/Prototype.md)
**Intent:** Create new objects by copying an existing instance (cloning).  
**Use when:** Construction is expensive, or you need many similar objects with small differences.  
**Key idea:** Copy then tweak; avoid repeated expensive initialization.

**References (read more):**
- [Wikipedia: Prototype pattern](https://en.wikipedia.org/wiki/Prototype_pattern)

### Structural patterns
<a id="structural-patterns"></a>

#### 6) Adapter
**Intent:** Convert the interface of one class into an interface expected by another class.  
**Use when:** You need to integrate incompatible APIs/classes.  
**Key idea:** “Wrap” one interface so clients can keep using what they expect.

#### 7) Facade
**Intent:** Provide a simplified interface to a complex subsystem.  
**Use when:** A subsystem has many moving parts and callers shouldn’t know details.  
**Key idea:** One entry point that hides complexity and reduces coupling.

#### 8) Decorator
**Intent:** Add responsibilities to objects dynamically without changing their class.  
**Use when:** You want flexible combinations of features (logging, metrics, compression, caching, auth checks).  
**Key idea:** Wrap the object; keep the same interface; compose behavior.

#### 9) Proxy
**Intent:** Provide a surrogate placeholder controlling access to another object.  
**Use when:** You need lazy initialization, access control, caching, remoting, or interception.  
**Key idea:** Control and route requests before they hit the real subject.

#### 10) Composite
**Intent:** Compose objects into tree structures to represent whole/part hierarchies.  
**Use when:** You want the same treatment for single objects and compositions of objects.  
**Key idea:** A component interface for both leaf and container nodes.

### Behavioral patterns
<a id="behavioral-patterns"></a>

#### 11) Observer
**Intent:** Define a dependency so that when one object changes, all dependents are notified.  
**Use when:** Changes must propagate to multiple listeners (events, UI updates, domain events).  
**Key idea:** Subject manages subscribers; dependents react to notifications.

#### 12) Strategy
**Intent:** Define a family of algorithms, encapsulate each one, and make them interchangeable.  
**Use when:** You choose behavior at runtime (pricing rules, sorting, routing, validation strategies).  
**Key idea:** Replace conditionals with polymorphism.

#### 13) Command
**Intent:** Encapsulate a request as an object, including the execution details.  
**Use when:** You need queuing, logging, undo/redo, batching, or remote execution.  
**Key idea:** Invoker calls a `Command`; command performs the action.

#### 14) State
**Intent:** Allow an object to alter its behavior when its internal state changes.  
**Use when:** Behavior depends heavily on state (order lifecycle, workflow, game entities).  
**Key idea:** Move state-specific logic into separate state objects.

#### 15) Chain of Responsibility
**Intent:** Pass a request along a chain of handlers until one handles it.  
**Use when:** Multiple handlers may process a request, and order matters.  
**Key idea:** Handlers decide to handle or forward.

#### 16) Iterator
**Intent:** Provide a way to access elements of an aggregate object sequentially without exposing its underlying representation.  
**Use when:** You need consistent traversal across different collection types.  
**Key idea:** An iterator abstracts iteration mechanics.

#### 17) Template Method
**Intent:** Define the skeleton of an algorithm, deferring some steps to subclasses.  
**Use when:** You want an algorithm framework with controlled variation.  
**Key idea:** Base class defines the flow; subclasses override specific steps.

---

## Where is the code?
This repo will implement each pattern in Java under:
`src/main/java/com/soabhaynu/design`

As we go, we will create per-pattern READMEs (notes + a small Java sketch) next to the code.

You can already find detailed notes for:
- `Singleton` (`src/main/java/com/soabhaynu/design/creational/singleton/Singleton.md`)
- `Builder` (`src/main/java/com/soabhaynu/design/creational/builder/Builder.md`)
- `Prototype` (`src/main/java/com/soabhaynu/design/creational/prototype/Prototype.md`)

## References (read more)
- [Gang of Four (GoF) Design Patterns (Wikipedia)](https://en.wikipedia.org/wiki/Design_Patterns)
- [Design pattern (Wikipedia)](https://en.wikipedia.org/wiki/Design_pattern)
- [Refactoring.Guru: Design Patterns (catalog)](https://refactoring.guru/design-patterns)
