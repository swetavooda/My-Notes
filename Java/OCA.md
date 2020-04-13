Java Notes
============

## Contents of the Notes
1) [Java Execution Flow Diagram](#Java-Execution-Flow-Diagram)

2) [JVM](#jvm)

3) [Classes vs Files](#Classes-vs-Files)

4) [Main method](#Main-method)
* [Command line arguments](#Command-line-arguments)



## Execution process of a java program 

![Java Execution Flow Diagram](java-imgs/Detailed-java-execution-flow-diagram.png)

1) the source code(.java file) is compiler using a compiler(javac) and byte code(.class files ) are generated.

2) when a class is excecuted (java abc) the class loader loads the .class file and bytecode is verified, the code is now going to get interpreted using a JIT complier(gives only needed lines to the interpreter to improve effieciency) and a interpreter.

3) this converts the code to machine language and is given to the OS for excecution.


**IMPORTANT POINTS**

* The byte code(.class file) is portable(platform independent).
* JVM is platform dependent (it coverts the byte code into the corresponding OS machine code).

## JVM

* The main method(startup of the Java process) is managed by the JVM. The JVM calls on the underlying system to allocate memory and CPU time, access files etc.
* JVM is platform dependent.

## Classes vs Files

* When we have two classes in the same file. Atmost one of the classes in the file is allowed to be public.
* If there are multiple classes and one of them is public then it needs to match the filename.
* If there are no public classes you can compile the code succesfully(with differnt file name also), but while running you must run the excecutable class file(one with main).
* The java sources code is stored in .java files (name same as class name).
* Byte code is stored in .class file with same name of the class.

## Main method
`public static void main(String args[])`
* the main method must be public and static.If the method is not static it becomes invisible to the JVM.
The main class is called without creading a object of the class, the JVM takes care of it.

* The parameters to the main method is a array of strings.(to take command line arguments)
It can be written in the following forms `String[] args`, `String args[]` or `String... args` and can use any name instead of "args".

#### Command line arguments

* spaces are used to separate the arguments.
* we need to use quotes to have spaces inside the arguments.

```
$ javac Zoo.java 
$ java Zoo "San Diego" Zoo 

```

* All command line argumnets are treated as String objects even if they represent other datatypes.


## Package Declarations and Imports
#### Packages
* Preventing naming conflicts. For example there can be two classes with name Employee in two packages, college.staff.cse.Employee and college.staff.ee.Employee
* Making searching/locating and usage of classes, interfaces, enumerations and annotations easier
* Providing controlled access: protected and default have package level access control. A protected member is accessible by classes in the same package and its subclasses. A default member (without any access specifier) is accessible by classes in the same package only.
* Packages can be considered as data encapsulation (or data-hiding).
**Notes**
*  Java puts classes in packages. These are logical groupings for classes. 
*  If it begins with java or javax, this means it came with the JDK
#### Wildcards
* Classes in the same package are often imported together. You can use a shortcut to import all the classes in a package:

```import java.util.*;    // imports java.util.Random among other things ```
* Every class in the java.util package is available to this program when Java compiles it. It doesn’t import child packages, fi elds, or methods; it imports only classes.
*  “static import” that imports other types.

#### Naming conflicts
Sometimes we can import a class that can be found in multiple places.
Example Date class, java provides implementations of `java.util.Date` and `java.sql.Date`
for the following object creation
```
public class Conflicts
{
Date date;
}
```
1) When the class is found in multiple packages, Java gives you the compiler error:
The type Date is ambiguous

```
import java.util.*;
import java.sql.*;//Does not compile
```
2) It takes precedence over any wildcards present
```
import java.util.Date; 
import java.sql.*;
```
3) error: a type with the same simple name is already defined by the single-type-import of Date
import java.sql.Date;
```
import java.util.Date; 
import java.sql.Date;

```
**Solution**
```
public class Conflicts { java.util.Date date; java.sql.Date sqlDate;
}

```
#### Creating a new package


## Constructors
* Constructor is a special type of method that creates a new object.
* the name of the constructor matches the name of the class, and there’s no return type
* if a constuctor is not defined the compiler provides a default constructor(This Java-created constructor is called the default constructor. Sometimes we call it the default no-arguments constructor ), but once a user defined constructor is provided the compiler doesnt provide the  default constructor anymore.
* constructors can be overloaded.
* The constructor is part of the initialization process, so it is allowed to assign final instance variables in it. By the time the constructor completes, all final instance variables must have been set.

#### Constructor chaining
```
Overloaded constructors often call each other. One common technique is to have each constructor add one parameter until getting to the constructor that does all the work. This approach is called constructor chaining. In this example, all three constructors are chained.
public class Mouse {   private int numTeeth;   private int numWhiskers;   private int weight;
   public Mouse(int weight) {     this(weight, 16); // calls constructor with 2 parameters   }   public Mouse(int weight, int numTeeth) {    this(weight, numTeeth, 6); // calls constructor with 3 parameters   }   public Mouse(int weight, int numTeeth, int numWhiskers) {     this.weight = weight;     this.numTeeth = numTeeth;     this.numWhiskers = numWhiskers;   }   public void print() {     System.out.println(weight + " " + numTeeth + " " + numWhiskers);   }   public static void main(String[] args) {     Mouse mouse = new Mouse(15);     mouse.print();   } }
This code prints 15 16 6. The main() method calls the constructor with one parameter. That constructor adds a second hard-coded value and calls the constructor with two parameters. That constructor adds one more hard-coded value and calls the constructor with three parameters. The three-parameter constructor assigns the instance variables.
```

#### constructors during inheritance
* during the creation on a derived class object :
    1) Base Class Constructor Called
    2) Derived Class Constructor Called
* If we want to call a parameterized constructor of the base class we must use `super` otherwise it will throw an error.
Because by default the default constructor of base class is called from the derived class constructor.
## Instance initializers
* the code blocks( {} ) appearing inside the class outside the methods are called instance initializers.
## Static initializers

#### Order of execution of Initialization blocks and constructor in Java

* Static initialization blocks will run whenever the class is loaded first time in JVM
* Initialization blocks run in the same order in which they appear in the program.
* Instance Initialization blocks are executed whenever the class is initialized and before constructors are invoked. They are typically placed above the constructors within braces.

**During inheritance**

```
// Java code to illustrate order of 
// execution of constructors, static 
// and initialization blocks 
class A{
  {
    System.out.println("Base 1st instance init"); 
  }
  static
  {
    System.out.println("Base 1st static init"); 
  }
  
  A()
  {
    System.out.println("Base class No argument constructor");
  }
  {
    System.out.println("Base 2nd instance init"); 
  }
}
class B extends A
{
{
    System.out.println("Derived 1st instance init"); 
  }
  static
  {
    System.out.println("Derived 1st static init"); 
  }
  B()
  {
    System.out.println("Derived class No argument constructor");
  }
  B(int x)
  {
    System.out.println("Derived class ONE argument constructor");
  }
  {
    System.out.println("Derived 2nd instance init"); 
  }
}
class GFG { 


	public static void main(String[] args) 
	{ 
		
		new B(8); 
        {
    System.out.println("============DONE========"); 
  }
        new B();
        {
    System.out.println("============DONE========"); 
  }
	} 
} 
```
output
```
Base 1st static init
Derived 1st static init
Base 1st instance init
Base 2nd instance init
Base class No argument constructor
Derived 1st instance init
Derived 2nd instance init
Derived class ONE argument constructor
============DONE========
Base 1st instance init
Base 2nd instance init
Base class No argument constructor
Derived 1st instance init
Derived 2nd instance init
Derived class No argument constructor
============DONE========
```






