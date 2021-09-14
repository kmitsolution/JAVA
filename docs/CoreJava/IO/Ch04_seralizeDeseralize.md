## Serialization and DeSerialization
Serialization is a mechanism of converting the state of an object into a byte stream. Deserialization is the reverse process where the byte stream is used to recreate the actual Java object in memory. This mechanism is used to persist the object.

![image](https://user-images.githubusercontent.com/84008107/133215864-db54f9f5-322e-477a-b884-9116ad690db4.png)

The byte stream created is platform independent. So, the object serialized on one platform can be deserialized on a different platform.

To make a Java object serializable we implement the java.io.Serializable interface.
The ObjectOutputStream class contains writeObject() method for serializing an Object.

```java
public final void writeObject(Object obj)
                       throws IOException
```                       
The <b>ObjectInputStream class</b> contains <b>readObject()</b> method for deserializing an object.

```java
public final Object readObject()
                  throws IOException,
               ClassNotFoundException
```

## Example 1
```java
// Java code for serialization and deserialization
// of a Java object
import java.io.*;

class Demo implements java.io.Serializable
{
	public int a;
	public String b;

	// Default constructor
	public Demo(int a, String b)
	{
		this.a = a;
		this.b = b;
	}

}

class Test
{
	public static void main(String[] args)
	{
		Demo object = new Demo(1, "geeksforgeeks");
		String filename = "file.ser";
		
		// Serialization
		try
		{
			//Saving of object in a file
			FileOutputStream file = new FileOutputStream(filename);
			ObjectOutputStream out = new ObjectOutputStream(file);
			
			// Method for serialization of object
			out.writeObject(object);
			
			out.close();
			file.close();
			
			System.out.println("Object has been serialized");

		}
		
		catch(IOException ex)
		{
			System.out.println("IOException is caught");
		}


		Demo object1 = null;

		// Deserialization
		try
		{
			// Reading the object from a file
			FileInputStream file = new FileInputStream(filename);
			ObjectInputStream in = new ObjectInputStream(file);
			
			// Method for deserialization of object
			object1 = (Demo)in.readObject();
			
			in.close();
			file.close();
			
			System.out.println("Object has been deserialized ");
			System.out.println("a = " + object1.a);
			System.out.println("b = " + object1.b);
		}
		
		catch(IOException ex)
		{
			System.out.println("IOException is caught");
		}
		
		catch(ClassNotFoundException ex)
		{
			System.out.println("ClassNotFoundException is caught");
		}

	}
}

```
## Example2

```java
// Java code for serialization and deserialization
// of a Java object
import java.io.*;

class Emp implements Serializable {
private static final long serialversionUID =
								129348938L;
	transient int a;
	static int b;
	String name;
	int age;

	// Default constructor
public Emp(String name, int age, int a, int b)
	{
		this.name = name;
		this.age = age;
		this.a = a;
		this.b = b;
	}

}

public class SerialExample {
public static void printdata(Emp object1)
	{

		System.out.println("name = " + object1.name);
		System.out.println("age = " + object1.age);
		System.out.println("a = " + object1.a);
		System.out.println("b = " + object1.b);
	}

public static void main(String[] args)
	{
		Emp object = new Emp("ab", 20, 2, 1000);
		String filename = "shubham.txt";

		// Serialization
		try {

			// Saving of object in a file
			FileOutputStream file = new FileOutputStream
										(filename);
			ObjectOutputStream out = new ObjectOutputStream
										(file);

			// Method for serialization of object
			out.writeObject(object);

			out.close();
			file.close();

			System.out.println("Object has been serialized\n"
							+ "Data before Deserialization.");
			printdata(object);

			// value of static variable changed
			object.b = 2000;
		}

		catch (IOException ex) {
			System.out.println("IOException is caught");
		}

		object = null;

		// Deserialization
		try {

			// Reading the object from a file
			FileInputStream file = new FileInputStream
										(filename);
			ObjectInputStream in = new ObjectInputStream
										(file);

			// Method for deserialization of object
			object = (Emp)in.readObject();

			in.close();
			file.close();
			System.out.println("Object has been deserialized\n"
								+ "Data after Deserialization.");
			printdata(object);

			// System.out.println("z = " + object1.z);
		}

		catch (IOException ex) {
			System.out.println("IOException is caught");
		}

		catch (ClassNotFoundException ex) {
			System.out.println("ClassNotFoundException" +
								" is caught");
		}
	}
}

```
