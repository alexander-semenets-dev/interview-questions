# interview-questions

## Java
### 1. Functional Interfaces in Java

Any interface with a SAM(Single Abstract Method) is a functional interface, and its implementation may be treated as lambda expressions.

Note that Java 8's default methods are not abstract and do not count: a functional interface may still have multiple default methods.

All functional interfaces are recommended to have an informative @FunctionalInterface annotation. This not only clearly communicates the purpose of this interface, but also allows a compiler to generate an error if the annotated interface does not satisfy the conditions.

#### Functions

The most simple and general case of a lambda is a functional interface with a method that receives one value and returns another. This function of a single argument is represented by the Function interface which is parameterized by the types of its argument and a return value:

public interface Function<T, R> { … }

The Function interface has also a default compose method that allows to combine several functions into one and execute them sequentially.

#### Primitive Function Specializations

Since a primitive type can’t be a generic type argument, there are versions of the Function interface for most used primitive types double, int, long, and their combinations in argument and return types:

* IntFunction, LongFunction, DoubleFunction: arguments are of specified type, return type is parameterized
* ToIntFunction, ToLongFunction, ToDoubleFunction: return type is of specified type, arguments are parameterized
* DoubleToIntFunction, DoubleToLongFunction, IntToDoubleFunction, IntToLongFunction, LongToIntFunction, LongToDoubleFunction — having both argument and return type defined as primitive types, as specified by their names

#### Two-Arity Function Specializations

To define lambdas with two arguments, we have to use additional interfaces that contain “Bi” keyword in their names: BiFunction, ToDoubleBiFunction, ToIntBiFunction, and ToLongBiFunction.

BiFunction has both arguments and a return type generified, while ToDoubleBiFunction and others allow you to return a primitive value.

#### Suppliers

The Supplier functional interface is yet another Function specialization that does not take any arguments. It is typically used for lazy generation of values.

Other specializations of Supplier functional interface include BooleanSupplier, DoubleSupplier, LongSupplier and IntSupplier, whose return types are corresponding primitives.

#### Consumers

As opposed to the Supplier, the Consumer accepts a generified argument and returns nothing. It is a function that is representing side effects.

There are also specialized versions of the Consumer — DoubleConsumer, IntConsumer and LongConsumer — that receive primitive values as arguments. More interesting is the BiConsumer interface.

Another set of specialized BiConsumer versions is comprised of ObjDoubleConsumer, ObjIntConsumer, and ObjLongConsumer which receive two arguments one of which is generified, and another is a primitive type.

#### Predicates

The Predicate functional interface is a specialization of a Function that receives a generified value and returns a boolean.

As in all previous examples, there are IntPredicate, DoublePredicate and LongPredicate versions of this function that receive primitive values.

#### Operators

Operator interfaces are special cases of a function that receive and return the same value type. The UnaryOperator interface receives a single argument.

One of the most interesting use cases of a BinaryOperator is a reduction operation.

Of course, there are also specializations of UnaryOperator and BinaryOperator that can be used with primitive values, namely DoubleUnaryOperator, IntUnaryOperator, LongUnaryOperator, DoubleBinaryOperator, IntBinaryOperator, and LongBinaryOperator.

https://www.baeldung.com/java-8-functional-interfaces

### 2. What is Constructor Chaining in Java

Java constructor chaining is a method of calling one constructor with the help of another while considering the present object.
It can be done in 2 ways –

* Within same class: It can be done using this() keyword for constructors in the same class.
* From base class: By using super() keyword to call a constructor from the base class.

https://data-flair.training/blogs/constructor-chaining-in-java/

### 3. DateTime API vs Date/Calendar

The new API is driven by three core ideas:

* Immutable-value classes. One of the serious weaknesses of the existing formatters (like java.util.SimpleDateFormat) in Java is that they aren’t thread-safe.
* Domain-driven design. The new API models its domain very precisely with classes that represent different use cases for Date and Time closely. This emphasis on domain-driven design offers long-term benefits around clarity and understandability, but you might need to think through your application’s domain model of dates when porting from previous APIs to Java SE 8.
* Separation of chronologies. The new API allows people to work with different “non-ISO-8601” calendaring systems, like one used in Japan or Thailand.

https://programminghints.com/2017/05/still-using-java-util-date-dont/

https://codeblog.jonskeet.uk/2017/04/23/all-about-java-util-date/

### 4. HashSet vs. TreeSet in Java

HashSet
* Null values can be added
* No fixed iteration order
* Heterogenous values are allowed
* Time complexity for insertion/deletion/retrieval: O(1)
* Implements the Set interface

TreeSet
* Nulls aren’t allowed
* Iteration over items is in natural order or a given Comparator is used
* Only homogenous values are allowed
* Time complexity for the same operations: O(log n)
* Implements the NavigableMapinterface

https://www.educative.io/edpresso/hashset-vs-treeset-in-java

### 5. Can we Overload or Override static methods in java?

We can declare static methods with the same signature in the subclass, but it is not considered overriding as there won’t be any run-time polymorphism. Hence the answer is ‘No’. If a derived class defines a static method with the same signature as a static method in the base class, the method in the derived class hides the method in the base class.

The following are some important points for method overriding and static methods in Java.

1) For class (or static) methods, the method according to the type of reference is called, not according to the object being referred, which means method call is decided at compile time.

2) For instance (or non-static) methods, the method is called according to the type of object being referred, not according to the type of reference, which means method calls is decided at run time.

3) An instance method cannot override a static method, and a static method cannot hide an instance method. For example, the following program has two compiler errors.

4) In a subclass (or Derived Class), we can overload the methods inherited from the superclass. Such overloaded methods neither hide nor override the superclass methods — they are new methods, unique to the subclass.

https://www.geeksforgeeks.org/can-we-overload-or-override-static-methods-in-java/

### 6. Method Overriding Rules

With respect to the method it overrides, the overriding method must follow following mandatory rules:

* It must have the same method name.
* It must have the same arguments.
* It must have the same return type. From Java 5 onward, the return type can also be a subclass (subclasses are a covariant type to their parents).
* It must not have a more restrictive access modifier (if parent --> protected then child --> private is not allowed).
* It must not throw new or broader checked exceptions.

And if both overriding methods follow the above mandatory rules, then they:

* May have a less restrictive access modifier (if parent --> protected then child --> public is allowed).
* May throw fewer or narrower checked exceptions or any unchecked exception.

Apart from the above rules, there are also some facts to keep in mind:

* Only inherited methods can be overridden. That means methods can be overridden only in child classes.
* Constructors and private methods are not inherited, so they cannot be overridden.
* Abstract methods must be overridden by the first concrete (non-abstract) subclass.
* final methods cannot be overridden.
* A subclass can use super.overridden_method() to call the superclass version of an overridden method.

https://dzone.com/articles/everything-about-method-overloading-vs-method-overriding

### 7. Method Overloading Rules

Two methods will be treated as overloaded if both follow the mandatory rules below:

* Both must have the same method name.
* Both must have different argument lists.

And if both methods follow the above mandatory rules, then they may or may not:

* Have different return types.
* Have different access modifiers.
* Throw different checked or unchecked exceptions.

https://dzone.com/articles/everything-about-method-overloading-vs-method-overriding

### 8. What is an Abstract Class and Abstract Method in Java?

* An abstract class is a class that is declared abstract
* Abstract classes cannot be instantiated
* Abstract classes can be subclassed
* It may or may not include abstract methods
* When an abstract class is subclassed, the subclass usually provides implementations for all of the abstract methods in its parent class
* If subclass doesn’t provide implementations then the subclass must also be declared abstract.

Of course yes. Declaring a class abstract only means that you don’t allow it to be instantiated on its own. You can’t have an abstract method in a non-abstract class.

### 9. What Is an Interface in Java?

### 10. Java String Pool

Thanks to the immutability of Strings in Java, the JVM can optimize the amount of memory allocated for them by storing only one copy of each literal String in the pool. This process is called interning.

When we create a String variable and assign a value to it, the JVM searches the pool for a String of equal value.

If found, the Java compiler will simply return a reference to its memory address, without allocating additional memory.

If not found, it'll be added to the pool (interned) and its reference will be returned.

When we create a String via the new operator, the Java compiler will create a new object and store it in the heap space reserved for the JVM.

Every String created like this will point to a different memory region with its own address.

We can manually intern a String in the Java String Pool by calling the intern() method on the object we want to intern.

Manually interning the String will store its reference in the pool, and the JVM will return this reference when needed.

Before Java 7, the JVM placed the Java String Pool in the PermGen space, which has a fixed size — it can't be expanded at runtime and is not eligible for garbage collection.

The risk of interning Strings in the PermGen (instead of the Heap) is that we can get an OutOfMemory error from the JVM if we intern too many Strings.

From Java 7 onwards, the Java String Pool is stored in the Heap space, which is garbage collected by the JVM. The advantage of this approach is the reduced risk of OutOfMemory error because unreferenced Strings will be removed from the pool, thereby releasing memory.

### 11. Instanceof With null

The Java instanceof operator always evaluates to false when a null variable is compared against any class or interface. Here is a Java instanceof example illustrating the comparison of null against a class:

Map<Object, Object> map = null;

boolean mapIsObject = map instanceof Map;

### 12. Race Conditions

A race condition occurs when two or more operations must execute in the correct
order, but the program has not been written so that this order is guaranteed to be
maintained.

Most of the time, this shows up in what’s called a data race, where one concurrent
operation attempts to read a variable while at some undetermined time another con‐
current operation is attempting to write to the same variable.

### 13. Deadlock

A deadlocked program is one in which all concurrent processes are waiting on one
another. In this state, the program will never recover without outside intervention.

It turns out there are a few conditions that must be present for deadlocks to arise. The conditions are now known as the Coffman Conditions and are the basis for techniques that help detect, prevent, and correct deadlocks.

The Coffman Conditions are as follows:

* Mutual Exclusion
A concurrent process holds exclusive rights to a resource at any one time.

* Wait For Condition
A concurrent process must simultaneously hold a resource and be waiting for an
additional resource.

* No Preemption
A resource held by a concurrent process can only be released by that process, so
it fulfills this condition.

* Circular Wait
A concurrent process (P1) must be waiting on a chain of other concurrent pro‐
cesses (P2), which are in turn waiting on it (P1), so it fulfills this final condition
too.

#### Livelock

Livelocks are programs that are actively performing concurrent operations, but these operations do nothing to move the state of the program forward.

Have you ever been in a hallway walking toward another person? She moves to one side to let you pass, but you’ve just done the same. So you move to the other side, but
she’s also done the same. Imagine this going on forever, and you understand livelocks.

#### Starvation

Starvation is any situation where a concurrent process cannot get all the resources it needs to perform work.

When we discussed livelocks, the resource each goroutine was starved of was a shared lock. Livelocks warrant discussion separate from starvation because in a live‐lock, all the concurrent processes are starved equally, and no work is accomplished.

More broadly, starvation usually implies that there are one or more greedy concurrent process that are unfairly preventing one or more concurrent processes from accomplishing work as efficiently as possible, or maybe at all.
