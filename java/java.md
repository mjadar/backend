# JAVA

- java est un langage de programmation OOP créé par James Gosling et Patrick Naughton employés de Sun Mycrosystems.

## How to read user inputs

```
Scanner scanner = new Scanner(System.in);
String name = scanner.nextLine();
scanner.close();
```

## Reference vs Object vs Instance vs Class

- a class is a blueprint to create a type
- object is an instanciation of a class

## Static vs Instance methods

- `static methods` are declared using a static modifier.
- `static methods` can't access instance methods and instance variables directly.

## Arrays, Java inbuilt Lists, Autoboxing and Unboxing

- [ARRAY] = `int [] myVariable = new int[10];`
- [ARRAY2]= `int[] myIntVar = {1,2,3,4,5}`
- myIntArray.length

## Inner class

```
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
System.out.println(inner.method1());
```

## Abstract class vs Interface

- [Abstract_Class] = similar to interfaces, cannot be instantiadted, and may contain a mix of methods declared with or without an implementation.
  - with [Abstact_Classes] you can declare fields that are not static and final, and define public, protected and private concrete methods.
  - provide a common definition of a base class that multiple derived classes can share.
- [Interface] = define what kind of operations an object can perform.
  - it forms a contract between the class and the outside world.
  - contain a mix of methods declared with or without an implementation.

## Java Generics

- equivalent to Templates

```
public class Team<T extends Player>{

} # only classes that extends Player class

public class Team<T>{

}
```

## Java Naming conventions

- the things you will name in java are: (packages, classes, interfaces, methods, constants, variables, type parameters).

## Comparable vs Comparator

- if sorting of objects needs to be based on natural order then use `Comparable` whereas if the sorting needs to be done on attributes of different objects, then use `Comparator`.
- the class implements directly Comparable.
- the class extends a cmpClass that implements Comparator. # Collections.sort(list, ratingCmpare);

## Collections

- `List interface` = It inhibits a list type data structure in which we can store the ordered collection of objects. It can have duplicate values.

- `ArrayList class` = It uses a dynamic array to store the duplicate element of different data types. The ArrayList class maintains the insertion order and is non-synchronized.

## immutable class

- immutable class in java means that once an object is created, we cannot change its content; The requirements are as follow:
  - The class must be declared as **final**.
  - Data members in the class must be declared **private** and **final**.
  - A parameterized constructor should initialize all the fields performing a deep copy so that data members can't be modified with object reference.
  - Deep copy of objects should be performeed in the getter methods to return a copy rather than returning the actual object reference.

## Override equals and hashcode

- always override haschode when you override equals.

## Wrapper Class

- is one that contains a variable that is a primitive data type, and wraps the primitive to provide functionality for interacting with it. It turns the primitive into an object.

## MAPS

- Hashmap : make no guarantees about the iteration order, elements inserted not in order.
- TreeMap : will ierate according to the natural ordering of the keys according to their compareTo() method.
- LinkedHashMap : will iterate in the order in which the entries were put into the map.

## Exceptions

- exceptions are unexpected events that occur at run time.

- [Checked] : is checked at compile time, exceptions under Throwable. `SQLException, IOExcpetion, InvocationTargetException, ClassNotFoundException`

- [Unchecked] : those that occur during the execution of the program. Referred to as Runtime exceptions. Ignored during compilation process. exceptions under Error and RuntimeException. `NullPointerException , ArrayIndexOutOfBound, IllegalArgumentException, IllegalStateException, NumberFormatException, ArithmeticException, `

## FileReader vs BufferedReader

- [FileReader] = used to read a file from a disk drive, directly reads the data from the character stream that originates from a file;

- [BufferedReader] = it creates an input buffer and allows the input to be read from the hard drive in large chunks of data rather than a byte at time. `Faster, Efficient`

- FileWriter //to write into a file.

## Serialization

- the process of translating a data structure or object into a format that can be stored and recreated.
- if a class we want to serialize it should have all the fields serializable.
- define serialVersionUID field : `private long serialVersionUID = 1L;`

## Concurrency

- [Process] = is a unit of execution that has its own memory space.
- each instance of a java Virtual Machine (JVM) runs as a process.
- each process has its own memory space of HEAP. And two java app cannot access heap of each other.

- Why use threads? Sometimes we want to perform a task that's going to take a long time. The code in the main thread executes in linear fashion, so the main thread won't be able to do anything else while it's waiting for the data.
- Concurrency means one task doesn't have to complete before another can start.

- Thread Join = the join() method which allows one thread to wait until another thread completes its execution. If t is a Thread object whose thread is currently executing, then t.join() will make sure that t is terminated before the next instruction is executed by the program.

- Thread interference = occurs when multiple thread tries to access the same resources.

- When you define a method `synchronized`, you are telling the thread that executes that method, i want this whole method to run before another thread can run it. Donc une fois que la méthode est appelée par un thread, aucun autre thread ne peux appeler la méthode avant que le premier thread n'en finisse;
- https://www.udemy.com/course/java-the-complete-java-developer-course/learn/lecture/5297652#learning-tools

- method or class is `thread safe` it means that the developer has synchronized all the critical sections within the code. So don't worry about thread interference.

- https://stackoverflow.com/questions/37026/java-notify-vs-notifyall-all-over-again `notify vs notifyall`

## Lambda expressions

- lambda expressions can be used with interfaces that has only one method to be implemented.
- Compiler is able to match lambda expression arguments list to a method.

- myList.forEeach(
  (n) -> sout(n);
  );

- if you want to reference a local variable defined outside of the anonymous class, it should be defined as final.

- **what happens when code runs with anonymous class** : an anonymous instance isn't created but instead, the lambda is treated as a nested block of code, and has same scope as a nested block.

## Functional Interfaces

- is an interface that contains only one abstract method. They can have only one functionality to exhibit.
- [Consumer] = this interface type of the functional interface take one argument and prints nothing. it has no return value. (use consumer.accept(aa);)
  `Consumer <Integer> consumer = (value) -> System.out.println(value); consumer.accept(maValue);`

- [Function] = A function is a type of functional interface in Java that receives only a single argument and returns a value after the required processing. use (function.apply(aa,bb);)

## Stream

- a sequence of elements supporting sequential and parallel aggregate operations
