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
