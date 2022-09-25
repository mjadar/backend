# Interviews

## Difference between Stack memory and Heap space

- stack memory is used for static memory allocation, such as primitive values inside a method. Stack grows when methods are called, and shrinks when they return. `StackOverFlowError` when stack is full.
- Heap memory is used for dynamic memory allocation, such as java objects. Object is stored in the heap, and the reference is stored in the stack. The JRE are also stored in the heap at run time.`StackOverFlowError` when memory allocated for heap is exceeded.
- Access data in heap is slower than in stack.
- Heap requires action of Garbage collector in order to free up unused objects.

## Nested classes

- there are two types of nested classes:
  - `Static nested class` = which doesn't directly have access to other members of the enclosing class, can access only static data memebers of the outer class, including private.
  - `Non static nested class` = the version referred to as inner class;

## What is anonymous inner class

- a class that has no name is known as an anonymous inner class in Java. It should be used if you have to override a method of class or interface.
- when you instanciate an abstract class or interface to override definition of a method.

## What is the Java virtual Machine

- JVM is a virtual machine that allows the computer to run java programs that have been compiled to bytecode.
- The bytecode is platform independent, and will run on any computer that hosts a JVM.
- JVM includes a just-in-time (JIT) compiler that converts the bytecode into machine language instructions.
