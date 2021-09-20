## Generic Collection
The generic collections are introduced in Java 5 Version. The generic collections disable the type-casting and there is no use of type-casting when it is used in generics. The generic collections are type-safe and checked at compile-time. These generic collections allow the datatypes to pass as parameters to classes. The Compiler is responsible for checking the compatibility of the types.

### Syntax
```
class<type>, interface<type>
```
### Type safety
Generics allows a single type of object.
```java
List list = new ArrayList(); // before generics
list.add(10);
list.add("100");
List<Integer> list1 = new ArrayList<Integer>(); // adding generics
list1.add(10);
list1.add("100"); // compile-time error.
```

### Type Casting
No need for type-casting while using generics.

```java
List<String> list = new ArrayList<String>();
list.add("Adithya");
String str = list.get(0); // no need of type-casting
```


### A Simple Java program to show multiple type parameters in Java Generics

```java
// We use < > to specify Parameter type
class Test<T, U>
{
	T obj1; // An object of type T
	U obj2; // An object of type U

	// constructor
	Test(T obj1, U obj2)
	{
		this.obj1 = obj1;
		this.obj2 = obj2;
	}

	// To print objects of T and U
	public void print()
	{
		System.out.println(obj1);
		System.out.println(obj2);
	}
}

// Driver class to test above
class Main
{
	public static void main (String[] args)
	{
		Test <String, Integer> obj =
			new Test<String, Integer>("GfG", 15);

		obj.print();
	}
}
```
### Java Generics Upper Bounded Wildcard
Upper bounded wildcards are used to relax the restriction on the type of variable in a method. Suppose we want to write a method that will return the sum of numbers in the list, so our implementation will be something like this.

```java
public static double sum(List<Number> list){
		double sum = 0;
		for(Number n : list){
			sum += n.doubleValue();
		}
		return sum;
	}
```	

Now the problem with above implementation is that it won’t work with List of Integers or Doubles because we know that List<Integer> and List<Double> are not related, this is when an upper bounded wildcard is helpful. We use generics wildcard with extends keyword and the upper bound class or interface that will allow us to pass argument of upper bound or it’s subclasses types.

The above implementation can be modified like the below program.


```java


import java.util.ArrayList;
import java.util.List;

public class GenericsWildcards {

	public static void main(String[] args) {
		List<Integer> ints = new ArrayList<>();
		ints.add(3); ints.add(5); ints.add(10);
		double sum = sum(ints);
		System.out.println("Sum of ints="+sum);
	}

	public static double sum(List<? extends Number> list){
		double sum = 0;
		for(Number n : list){
			sum += n.doubleValue();
		}
		return sum;
	}
}
```
It’s similar like writing our code in terms of interface, in the above method we can use all the methods of upper bound class Number. Note that with upper bounded list, we are not allowed to add any object to the list except null. If we will try to add an element to the list inside the sum method, the program won’t compile.
