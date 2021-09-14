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
