#java
* [git cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links)
* [Java API](https://docs.oracle.com/javase/8/docs/api/)
* [Geeks for Geeks](https://www.geeksforgeeks.org/java/)

* to print a object of a class without getting hashcode and hexadecimal [solution](//https://stackoverflow.com/questions/13498179/output-of-system-out-printlnobject)

## Data types

[https://www.geeksforgeeks.org/type-conversion-java-examples/]

UNI code in java - it takes 2 bytes for a character(to represent different scripts)

datatype|space(bytes)|
---------|-----|
short|2|
int|4|
float|4|
long|8|
double|8|
boolean|-|

double and float store exponents

* narrowing error

```
class Test2
{
    public static void main(String [] args)
    {
        byte b=25;
        b=b+10;//narroeing error
        /* whenever an operation is performed on a byte,short,char it is automatically converted/upgraded to int
        right hand side int left hand side byte*/
        System.out.println("Byte value: "+b);
    }
}
```
## Type promotion in Expressions

While evaluating expressions, the intermediate value may exceed the range of operands and hence the expression value will be promoted. Some conditions for type promotion are:

* Java automatically promotes each byte, short, or char operand to int when evaluating an expression.
* If one operand is a long, float or double the whole expression is promoted to long, float or double respectively.
* all compoud operators perform implicit type casting

```
class Test2
{
    public static void main(String [] args)
    {
        byte b=25;
        b+=10;//implicit conversion.(b=(byte)(b+10))
        System.out.println("Byte value: "+b);
    }
}
```

* byte short int long - rapping around.(byte can hold -128 to 127)

```
class Test2
{
    public static void main(String [] args)
    {
        byte b=(byte)129;
        System.out.println("Byte value: "+b);
    }
}
 
```
* int to byte and double to byte
 
 
```
//Java program to illustrate Conversion of int and double to byte 
class Test 
{ 
	public static void main(String args[]) 
	{ 
		byte b; 
		int i = 257; 
		double d = 323.142; 
		System.out.println("Conversion of int to byte."); 
		
		//i%256 
		b = (byte) i; 
		System.out.println("i = " + i + " b = " + b); 
		System.out.println("\nConversion of double to byte."); 
		
		//d%256 
		b = (byte) d; 
		System.out.println("d = " + d + " b= " + b); 
	} 
} 

```
* abstract class refer (AbstractClass.java)
* interface is an abstract class with all abstact methods.
    * the reference to an interface can point to any object of that class which implementsthe interface.
    * one interface can extend another interface.
    * anonymous class has only one instance of the Class/Interface.
    * Functional interface is an interface with only one method(directly or indirectly)/doesnt inherit something.
* final is  a keyword used to restrict inheritance from this class.

# Static methods

## Static keyword 
[https://www.geeksforgeeks.org/static-keyword-java/]
static members can be accesed before instantiating a class

### static blocks

If you need to do computation in order to initialize your static variables, you can declare a static block that gets executed exactly once, when the class is first loaded. Consider the following java program demonstrating use of static blocks.

### static variables

* we can create static variables at class level only
* static block and static variables are excecuted in order they are present in a program

### static methods

When a method is declared with static keyword, it is known as static method. The most common example of a static method is main( ) method.As discussed above, Any static member can be accessed before any objects of its class are created, and without reference to any object.Methods declared as static have several restrictions:

* They can only directly call other static methods.
* They can only directly access static data.
* They cannot refer to this or super in any way.

* static method belongs to class and not instance
* static method can access only static variables
* static methods cannot be overriden instance methods and vice-versa aas well
* polymorphism does not work on static method

### Static classes
[https://www.geeksforgeeks.org/static-class-in-java/]

### default of boolean data type is false

## Strings

lets say s1 is a reference to kmit
lets say s2 is also a reference to kmit
but when we type String s2="kmit";
jvm checks if "kmit" is present in the literal pool
since it is already existing,s2 will act as a reference to the same "kmit" and thereby output is true

charAt

in C++, all string must be terminated with \0
in java nthg is required

the method called length()is used to calculate the len of string


compareTo gives lexicographic difference i.e, compares ASCII values
read comapreToIgnorecase()
contains()
copyValueOf()
endsWith()
ends with checks the suffix of the string,returns boolean

char and byte are diff

byte[]//read this
hashCode()

## Exception handling

[https://www.geeksforgeeks.org/exceptions-in-java/]
Exceptions are of two types
1) runtime exeptions/unchecked exceptions
    * arithmetic
    * array out of bounds
    * etc
2) Checked exceptions/compile time exception
    all other kind of exceotions more than 95% exceptions are checked exceptions.
* check file not found exception
* check exceptions should either be caugth or by reporting the exception{ignore(by throw)}
when to choose to ignore a exception
* when we want to propogate the exception to another functon(say main) to handle the exception globally rether locally.
to make programmer aware that there would be an exception
 throws to report , throw instantiate exception
 
 
# wrapper classes
Boolean
Float
Long
Double

**doubts**
* if a program in interface we use lambda programming
* default interfaces
## threads
 * runnable vs callable
    run method shouldnt throw an exception/duck an exception
    call method can duck an exception
    
    (refer geeks for geeks callable future)
* thread can only accept an objec ehich implements a runaable interface
* thread pooling
(refer geeks for geeks thread pool)


