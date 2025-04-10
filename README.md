# Abstract Factory (KIT)

- **Intent:** Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
- **Motivation:** To support multiple look-and-feel standards in a UI toolkit without hard-coding specific widget classes, making it easy to change the look and feel later.
- **Participants:**
  - **AbstractFactory:** Declares creation interfaces.
  - **ConcreteFactory:** Implements concrete product creation.
  - **AbstractProduct:** Declares product interfaces.
  - **ConcreteProduct:** Implements products.
  - **Client:** Uses abstract interfaces.
- **Consequences:** Isolates concrete classes and makes exchanging product families easy, promoting consistency but making it difficult to support new kinds of products.
- **Applicability:**
  - When a system should be independent of product creation, composition, and representation.
  - When configured with multiple product families.
  - To enforce usage constraints of related products.
- **Example**
  Abstract Factory: A user interface toolkit that supports multiple look-and-feel standards, such as Motif and Presentation Manager, uses an abstract WidgetFactory to create families of related widgets (like scroll bars, windows, and buttons) without specifying their concrete classes. For each look-and-feel (e.g., Motif), there is a concrete subclass of WidgetFactory (e.g., MotifWidgetFactory) that creates the corresponding concrete widgets (e.g., MotifScrollBar, MotifButton).
- **Implentation**
  - Prototype
  - Singleton
  - Factory

# Adapter (Wrapper)

- **Intent:** Convert the interface of a class into another interface clients expect, enabling collaboration between classes with incompatible interfaces.
- **Motivation:** To reuse an existing class whose interface doesn't match the required domain-specific interface, such as using `TextView` as a `Shape` in a drawing editor.
- **Participants:**
  - **Target:** Defines the required interface.
  - **Client:** Uses the Target interface.
  - **Adaptee:** Has the existing interface.
  - **Adapter:** Adapts the Adaptee to the Target.
- **Consequences:**
  - Class adapters commit to a concrete adapter and allow overriding Adaptee behavior.
  - Object adapters work with multiple Adaptees but make overriding harder.
- **Applicability:**
  - When you want to use an existing class with a mismatched interface.
  - When creating a reusable class that can cooperate with unrelated or unforeseen classes.
- **Example**
  Adapter: A drawing editor that uses a Shape interface for graphical objects wants to reuse a TextView class for displaying and editing text, but TextView has an incompatible interface. A TextShape class can act as an adapter, either by inheriting from both Shape and TextView (class adapter) or by containing a TextView instance and implementing the Shape interface by delegating to the TextView object (object adapter).
- **Related Patterns**
  - Bridge
  - Decorator
  - Proxy

# Bridge (Handle/Body)

- **Intent:** Decouple an abstraction from its implementation so that the two can vary independently.
- **Motivation:** To avoid a permanent binding between an abstraction and its implementation caused by inheritance, allowing for easier modification, extension, and independent reuse (e.g., a portable `Window` abstraction).
- **Participants:**
  - **Abstraction:** Defines the interface and holds an Implementor reference.
  - **RefinedAbstraction:** Extends the Abstraction.
  - **Implementor:** Defines the implementation interface.
  - **ConcreteImplementor:** Provides platform-specific implementations.
- **Consequences:** Decouples interface and implementation, improves extensibility, and hides implementation details from clients.
- **Applicability:**
  - When you want to avoid a permanent binding between abstraction and implementation.
  - When both should be extensible.
  - When implementation changes shouldn't impact clients.
- **Example**
  Bridge: Implementing a portable Window abstraction in a user interface toolkit that needs to work on different platforms like the X Window System and Presentation Manager. The Window abstraction and its platform-specific implementations (XWindowImp, PMWindowImp) are in separate class hierarchies, allowing them to vary independently.
- **Related Patterns**
  - Abstract Factory
  - Adapter

# Builder

- **Intent:** Separate the construction of a complex object from its representation so that the same construction process can create different representations.
- **Motivation:** To allow an algorithm for creating a complex object (like an RTF reader) to produce various representations (ASCII, TeX, widget) by using different converter objects.
- **Participants:**
  - **Builder:** Defines an interface for creating product parts.
  - **ConcreteBuilder:** Implements the interface and assembles the product.
  - **Director:** Constructs the object using the Builder interface.
  - **Product:** The complex object being built.
- **Consequences:** Allows varying a product's internal representation, isolates construction and representation code, and provides finer control over the construction process.
- **Applicability:**
  - When the algorithm for creating a complex object should be independent of its parts and assembly.
  - When the construction process must allow different representations.
- **Example**
  Builder: An RTFReader that can convert RTF documents into various text formats (like plain ASCII or a text widget) uses a TextConverter interface. Concrete TextConverter subclasses (e.g., ASCIIConverter, TeXConverter, TextWidgetConverter) act as builders, responsible for creating and assembling the different text representations. The RTFReader (the director) uses the TextConverter to perform the conversion while parsing the RTF document.

# Chain of Responsibility

- **Intent:** Avoid coupling the sender of a request to its receiver by giving multiple objects a chance to handle the request and passing it along a chain.
- **Motivation:** To handle requests by one of several objects without the sender knowing explicitly who will handle it (e.g., a context-sensitive help facility where different UI elements may provide help).
- **Participants:**
  - **Handler:** Defines an interface for handling requests and optionally the successor link.
  - **ConcreteHandler:** Handles or forwards requests.
  - **Client:** Initiates the request to the chain.
- **Consequences:** Reduces coupling between sender and receiver and adds flexibility in assigning responsibilities, but request receipt isn't guaranteed.
- **Applicability:**
  - When more than one object may handle a request, and the handler isn’t known a priori.
  - When you want to issue a request without specifying the receiver.
  - When the set of handlers should be dynamic.
- **Example**
  Chain of Responsibility: A context-sensitive help facility for a GUI where a help request from a button can be handled by the button itself, its parent dialog box, or the main window, depending on the specificity of the help information available. The request is passed along a chain of HelpHandler objects until one is able to handle it.
- **Related Patterns**
  - Composite

# Command

- **Intent:** Encapsulate a request as an object, allowing parameterization of clients with different requests, queuing, logging, and supporting undoable operations.
- **Motivation:** To enable UI toolkit objects like buttons to make requests of unspecified application objects by turning the request itself into an object that can be stored and passed around.
- **Participants:**
  - **Command:** Declares an interface for executing an operation.
  - **ConcreteCommand:** Binds a Receiver to an action.
  - **Client:** Creates a ConcreteCommand and sets its receiver.
  - **Invoker:** Asks the command to execute.
  - **Receiver:** Performs the operation.
- **Consequences:** Decouples invoker and receiver, makes commands first-class objects that can be manipulated, and allows for easy addition of new commands.
- **Applicability:**
  - When you want to parameterize objects by an action to perform.
  - When you need to specify, queue, and execute requests at different times.
  - When supporting undo functionality.
- **Example**
  Command: User interface toolkits use objects like buttons and menus to carry out requests in response to user input. The actual action to be performed is encapsulated in a Command object, allowing the toolkit objects to make requests of unspecified application objects without knowing the details of the operation or the receiver. For example, a PasteCommand encapsulates the action of pasting content.

# Composite

- **Intent:** Compose objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.
- **Motivation:** To enable users in graphics applications to build complex diagrams from simple components and treat both individual primitives and groups of primitives in the same way.
- **Participants:**
  - **Component:** Declares the interface for objects in the composition and for managing children.
  - **Leaf:** Represents primitive objects.
  - **Composite:** Represents containers of components.
  - **Client:** Interacts with objects through the Component interface.
- **Consequences:** Defines hierarchies of primitive and composite objects, simplifies the client by providing uniform treatment, and makes adding new component types easier.
- **Applicability:**
  - When you want to represent part-whole hierarchies of objects.
  - When clients should ignore the difference between individual and composite objects.
- **Example**
  Composite: Graphics applications that allow users to build complex diagrams from simple components like Text and Lines. These primitives and containers (Picture) that group them share a common interface (Graphic) allowing clients to treat individual objects and compositions uniformly.

# Decorator

- **Intent:** Attach additional responsibilities to an object dynamically, providing a flexible alternative to subclassing for extending functionality.
- **Motivation:** To add properties like borders or behaviors like scrolling to individual UI components at runtime without affecting other objects or creating a proliferation of subclasses.
- **Participants:**
  - **Component:** Defines the interface for objects that can be decorated.
  - **ConcreteComponent:** The object being decorated.
  - **Decorator:** Maintains a reference to a Component and conforms to its interface.
  - **ConcreteDecorator:** Adds responsibilities.
- **Consequences:** Offers more flexibility than static inheritance and avoids feature-laden classes high in the hierarchy, but a decorator and its component are not identical.
- **Applicability:**
  - To add responsibilities to individual objects dynamically and transparently.
  - For responsibilities that can be withdrawn.
  - When extension by subclassing is impractical.
- **Example**
  Decorator: Adding borders or scrolling functionality to user interface components dynamically. A BorderDecorator or ScrollDecorator wraps a VisualComponent (like a TextView) and adds the extra responsibility without altering the TextView's basic interface.

# Facade

- **Intent:** Provide a unified interface to a set of interfaces in a subsystem, making the subsystem easier to use.
- **Motivation:** To reduce complexity and minimize dependencies between subsystems by offering a single, simplified interface to the more general facilities of a complex subsystem (e.g., a Compiler facade).
- **Participants:**
  - **Facade:** Knows the subsystem classes responsible for a request and delegates to them.
  - **Subsystem classes:** Implement the functionality and are unaware of the facade.
- **Consequences:** Shields clients from subsystem components, reduces the number of objects clients interact with, and promotes weak coupling between subsystems and clients.
- **Applicability:**
  - When you want to provide a simple interface to a complex subsystem.
  - When there are many dependencies between clients and implementation classes.
  - When you want to layer subsystems.
- **Example**
  Facade: A compiler subsystem with complex classes like Scanner, Parser, and CodeGenerator can provide a simplified Compiler class as a facade. This facade offers a single, higher-level interface to the compiler's functionality, making it easier for most clients to use without needing to interact directly with the more intricate subsystem components.

# Factory Method

- **Intent:** Define an interface for creating an object, but let subclasses decide which class to instantiate, thereby deferring instantiation to subclasses.
- **Motivation:** A framework (like for document applications) needs to create objects (like Documents) but doesn't know the specific application-specific subclass to instantiate until runtime.
- **Participants:**
  - **Product:** Defines the interface of created objects.
  - **ConcreteProduct:** Implements the Product interface.
  - **Creator:** Declares the factory method.
  - **ConcreteCreator:** Overrides the factory method to return a ConcreteProduct.
- **Consequences:** Provides hooks for subclasses to customize object creation and can connect parallel class hierarchies.
- **Applicability:**
  - When a class can't anticipate the class of objects it must create.
  - When a class wants its subclasses to specify the objects it creates.
  - When delegating responsibility to helper subclasses.
- **Example**
  Factory Method: A framework for applications that can present multiple documents uses abstract Application and Document classes. Concrete application subclasses (like DrawingApplication) override an abstract CreateDocument factory method in the Application class to return the appropriate concrete Document subclass (like DrawingDocument) when a new document is needed.

# Flyweight

- **Intent:** Use sharing to support large numbers of fine-grained objects efficiently.
- **Motivation:** To reduce memory usage and improve performance in applications that use a large number of objects with shared intrinsic state, such as representing individual characters in a document.
- **Participants:**
  - **Flyweight:** Declares an interface for receiving and acting upon extrinsic state.
  - **ConcreteFlyweight:** Implements the interface and stores intrinsic state.
  - **UnsharedConcreteFlyweight:** A flyweight that is not shared.
  - **FlyweightFactory:** Creates and manages flyweight objects.
  - **Client:** Maintains extrinsic state.
- **Consequences:** Can significantly reduce memory consumption by sharing objects, but introduces runtime costs for managing and passing extrinsic state.
- **Applicability:**
  - When an application uses a large number of objects.
  - When storage costs are high.
  - When most object state can be made extrinsic.
  - When object identity is not crucial.
- **Example**
  Flyweight: In a document editor, instead of creating a separate object for each character, a Character flyweight object can be shared across multiple contexts. The intrinsic state (like the font and character code) is stored in the Character object, while the extrinsic state (like position) is passed to it when needed.
- **Related pattern**
  - Cmposite
  - State
  - Strategy

# Interpreter

- **Intent:** Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.
- **Motivation:** When a particular problem can be expressed as sentences in a simple language, and an interpreter can solve the problem by interpreting these sentences (e.g., regular expressions for pattern matching).
- **Participants:**
  - **AbstractExpression:** Defines an interface for interpreting.
  - **TerminalExpression:** Implements interpretation for terminal symbols.
  - **NonterminalExpression:** Implements interpretation for nonterminal symbols.
  - **Context:** Holds global information.
  - **Client:** Builds the syntax tree and invokes interpretation.
- **Consequences:**
  - Easy to change and extend the grammar.
  - Straightforward implementation for simple grammars.
  - Complex grammars can become hard to maintain and may be inefficient.
- **Applicability:**
  - When there is a language to interpret.
  - When statements can be represented as abstract syntax trees.
  - Best suited for simple grammars where efficiency is not critical.
- **Example**
  Interpreter: Using regular expressions to specify patterns of strings. Each rule in the regular expression grammar can be represented by a class (e.g., LiteralExpression, AlternationExpression), and an interpreter uses these representations to match patterns against strings.

# Iterator (Cursor)

- **Intent:** Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
- **Motivation:** To allow traversal of collection elements without revealing the internal structure and to support multiple simultaneous traversals or different traversal algorithms.
- **Participants:**
  - **Iterator:** Defines an interface for accessing and traversing elements.
  - **ConcreteIterator:** Implements the interface and tracks the current position.
  - **Aggregate:** Defines an interface for creating an Iterator.
  - **ConcreteAggregate:** Returns a ConcreteIterator instance.
- **Consequences:** Supports variations in aggregate traversal, simplifies the Aggregate interface, and allows multiple pending traversals.
- **Applicability:**
  - To access an aggregate object's contents without exposing its internal representation.
  - To support multiple traversals of aggregate objects.
  - To provide a uniform traversal interface for different aggregate structures.
- **Example**
  Iterator: A List aggregate object provides a way to access its elements sequentially without exposing its internal structure by using a separate ListIterator object. The ListIterator keeps track of the current position and allows traversal through the list's elements.
- **Related Patterns**
  - Composite
  - Factory Method

# Mediator

- **Intent:** Define an object that encapsulates how a set of objects interact, promoting loose coupling by preventing objects from referring to each other explicitly.
- **Motivation:** To reduce complex interdependencies between objects by centralizing their interaction logic in a separate mediator object (e.g., coordinating widgets in a dialog box).
- **Participants:**
  - **Mediator:** Defines an interface for colleague communication.
  - **ConcreteMediator:** Implements the cooperative behavior and knows its colleagues.
  - **Colleague classes:** Communicate with the mediator rather than each other.
- **Consequences:** Limits subclassing related to interactions, decouples colleagues, simplifies object protocols, and centralizes control.
- **Applicability:**
  - When a set of objects communicate in complex ways.
  - When reusing an object is difficult due to its references to others.
  - When distributed behavior should be customizable without extensive subclassing.
- **Example**
  Mediator: In a dialog box with various widgets like buttons and entry fields, a DialogDirector object acts as a mediator to coordinate the interactions between these widgets. For example, the mediator can disable a button when a certain entry field is empty, thus centralising the control logic.

# Memento

- **Intent:** Without violating encapsulation, capture and externalize an object’s internal state so that the object can be restored to this state later.
- **Motivation:** To implement undo mechanisms and checkpoints by saving an object's state externally without exposing its internal details, thereby preserving encapsulation.
- **Participants:**
  - **Memento:** Stores the Originator's internal state.
  - **Originator:** Creates mementos and uses them to restore its state.
  - **Caretaker:** Responsible for safekeeping mementos.
- **Consequences:** Preserves encapsulation boundaries and simplifies the Originator, but managing mementos can be expensive.
- **Applicability:** When a snapshot of an object's state must be saved for later restoration without violating its encapsulation.
- **Example**
  Memento: An undo mechanism in an application can use a Memento object to store a snapshot of an object's internal state (SolverState). The originator (ConstraintSolver) creates the memento, and the caretaker (the undo mechanism) stores it and can later return it to the originator to restore its previous state, without violating encapsulation.

# Observer (Publish-Subscribe / Dependents)

- **Intent:** Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
- **Motivation:** To maintain consistency between related objects (e.g., a spreadsheet and a chart) without tight coupling, allowing for independent reuse of subjects and observers.
- **Participants:**
  - **Subject:** Knows its observers and provides interfaces for attaching/detaching them.
  - **Observer:** Defines an updating interface.
  - **ConcreteSubject:** Maintains state and notifies observers.
  - **ConcreteObserver:** Maintains a reference to the subject and updates itself.
- **Consequences:** Allows varying subjects and observers independently, supports broadcast communication, but can lead to unexpected updates.
- **Applicability:**
  - When an abstraction has two dependent aspects that should be encapsulated separately.
  - When a change in one object requires changes in an unknown number of others.
  - When an object should notify others without knowing who they are.
- **Example**
  Observer: A spreadsheet object and a bar chart object both display data from the same underlying application data object. When the data in the spreadsheet changes (the subject), the bar chart (an observer) is automatically notified and updates its presentation.
- **Related pattern**
  - Singleton
  - Mediator

# Prototype

- **Intent:** Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.
- **Motivation:** To avoid building a class hierarchy of factories or when the specific classes to instantiate are determined at runtime, allowing for new product types by simply registering a prototype.
- **Participants:**
  - **Prototype:** Declares an interface for cloning.
  - **ConcretePrototype:** Implements the cloning operation.
  - **Client:** Creates new objects by asking a prototype to clone itself.
- **Consequences:** Allows adding and removing products at runtime, specifying new objects by varying values or structure, and reduces the need for subclassing.
- **Applicability:**
  - When a system should be independent of how its products are created, composed, and represented.
  - When classes are specified at runtime.
  - To avoid parallel factory hierarchies.
- **Example**
  Prototype: A graphical editor framework uses a GraphicTool that needs to create instances of application-specific Graphic subclasses (like Staff, WholeNote). Instead of creating new instances directly, the GraphicTool clones a prototypical instance of the required Graphic subclass.

# Proxy

- **Intent:** Provide a surrogate or placeholder for another object to control access to it.
- **Motivation:** To control access to a real object, such as delaying the creation of an expensive object until it's needed (virtual proxy), accessing a remote object (remote proxy), or controlling access based on permissions (protection proxy).
- **Participants:**
  - **Proxy:** Maintains a reference to the RealSubject, provides the same interface, and controls access.
  - **Subject:** Defines the common interface.
  - **RealSubject:** The actual object being represented.
- **Consequences:** Introduces a level of indirection that can provide various benefits like lazy instantiation, remote access, and access control.
- **Applicability:**
  - Whenever a more versatile or sophisticated reference to an object than a simple pointer is needed.
  - For remote objects, expensive objects requiring on-demand creation, or controlled access.
- **Example**
  Proxy: A document editor that can embed large raster images uses an ImageProxy as a placeholder for the actual Image object. The proxy handles the creation of the real Image only when it is needed (e.g., when it becomes visible), thus deferring the expensive creation process.

# Singleton

- **Intent:** Ensure a class only has one instance, and provide a global point of access to it.
- **Motivation:** For classes where exactly one instance should exist (e.g., a printer spooler, configuration manager) and needs to be globally accessible.
- **Participants:**
  - **Singleton:** Defines an `Instance` operation that allows clients to access its unique instance and may be responsible for creating the instance.
- **Consequences:** Provides controlled access to the single instance, reduces namespace pollution compared to global variables, and permits refinement of operations and representation.
- **Applicability:**
  - When there must be exactly one instance of a class.
  - When it must be accessible to clients from a well-known access point.
  - When the sole instance should be extensible by subclassing.
- **Example**
  Singleton: A printer spooler in a system should have only one instance. The PrinterSpooler class ensures that only one instance of itself is created and provides a global point of access to that instance.
- **Related Patterns**
  - Builder
  - Abstract Factory
  - Builder
  - Prototype

# State

- **Intent:** Allow an object to alter its behavior when its internal state changes, making the object appear to change its class.
- **Motivation:** When an object's behavior is dependent on its state, and this behavior needs to change at runtime based on the current state, avoiding large conditional statements (e.g., in a TCPConnection).
- **Participants:**
  - **Context:** Defines the interface of interest and maintains a State object.
  - **State:** Defines an interface for state-specific behavior.
  - **ConcreteState:** Subclasses implement behavior for specific states.
- **Consequences:** Localizes state-specific behavior, partitions behavior for different states, makes state transitions explicit, and allows state objects to be shared.
- **Applicability:**
  - When an object's behavior depends on its state and must change at runtime.
  - When operations involve large, multipart conditional statements based on state.
- **Example**
  State: A TCPConnection object can be in different states (e.g., Established, Listening, Closed), and its behaviour changes based on its current state. The TCPConnection object maintains a TCPState object representing its current state and delegates state-specific requests to this object.

# Strategy (Policy)

- **Intent:** Define a family of algorithms, encapsulate each one, and make them interchangeable, allowing the algorithm to vary independently from clients that use it.
- **Motivation:** To avoid hard-wiring algorithms into classes that need them, making it easier to switch algorithms, add new ones, and reduce complexity (e.g., different line-breaking algorithms).
- **Participants:**
  - **Strategy:** Declares a common interface for algorithms.
  - **ConcreteStrategy:** Implements a specific algorithm.
  - **Context:** Is configured with a ConcreteStrategy object and uses its interface.
- **Consequences:** Creates families of related algorithms, offers an alternative to subclassing for behavior variation, and eliminates conditional statements, though clients must be aware of different Strategies.
- **Applicability:**
  - When many related classes differ only in their behavior.
  - When you need different variants of an algorithm.
  - To avoid exposing algorithm-specific data.
  - To replace many conditional statements.
- **Example**
  Strategy: Different algorithms for breaking a stream of text into lines can be encapsulated in separate Strategy classes (e.g., SimpleCompositor, TeXCompositor). A Composition object (the context) can then be configured with a specific Strategy to determine how it performs line breaking, allowing the algorithm to vary independently of the Composition.
- **Related pattern**
  - Flyweight

# Template Method

- **Intent:** Define the skeleton of an algorithm in an operation, deferring some steps to subclasses, allowing subclasses to redefine certain steps without altering the algorithm's structure.
- **Motivation:** To implement the invariant parts of an algorithm once in a superclass and allow subclasses to provide specific implementations for the variable parts, promoting code reuse (e.g., in framework classes).
- **Participants:**
  - **AbstractClass:** Defines abstract primitive operations and the template method.
  - **ConcreteClass:** Implements the primitive operations to carry out subclass-specific steps.
- **Consequences:** Template methods are a fundamental technique for code reuse, particularly important in class libraries for factoring out common behavior.
- **Applicability:**
  - To implement the invariant parts of an algorithm once and leave the variable parts to subclasses.
  - To factor out common behavior and avoid code duplication.
  - To control subclass extensions.
- **Example**
  Template Method: An application framework with Application and Document classes defines the overall process of opening a document in a template method. Subclasses like DrawingApplication and DrawingDocument then override specific steps (e.g., CanOpenDocument, DoCreateDocument, DoRead) to provide application-specific behaviour without changing the overall algorithm structure.

# Visitor

- **Intent:** Represent an operation to be performed on the elements of an object structure, allowing you to define a new operation without changing the classes of the elements.
- **Motivation:** When you need to perform many distinct and unrelated operations on objects in a complex structure with differing interfaces, and you want to avoid "polluting" the object classes with these operations (e.g., in a compiler's abstract syntax tree).
- **Participants:**
  - **Visitor:** Declares a `Visit` operation for each ConcreteElement.
  - **ConcreteVisitor:** Implements each `Visit` operation.
  - **Element:** Defines an `Accept` operation.
  - **ConcreteElement:** Implements `Accept` by calling the visitor's corresponding `Visit`.
  - **ObjectStructure:** Can enumerate its elements.
- **Consequences:** Makes adding new operations easy by encapsulating related operations in a visitor, but adding new ConcreteElement classes becomes harder.
- **Applicability:**
  - When an object structure contains many classes with differing interfaces.
  - When you want to perform operations dependent on their concrete classes without modifying the classes.
  - When many distinct operations are needed.
- **Example**
  Visitor: A compiler represents programs as abstract syntax trees. Different operations like type-checking and code generation need to be performed on these trees. Instead of adding these operations to the node classes of the abstract syntax tree, a separate Visitor object (TypeCheckingVisitor, CodeGeneratingVisitor) can be created to encapsulate the operations for each node type. The nodes then accept the visitor, allowing it to perform the specific operation for that node.
