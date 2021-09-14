## Exception Handling
Exception Handling is a mechanism to handle runtime errors such as ClassNotFoundException, IOException, SQLException, RemoteException, etc.

## Advantages of Exception Handling
The core advantage of exception handling is to maintain the normal flow of the application. An exception normally disrupts the normal flow of the application; that is why we need to handle exceptions. Let's consider a scenario:
```
statement 1;  
statement 2;  
statement 3;  
statement 4;  
statement 5;//exception occurs  
statement 6;  
statement 7;  
statement 8;  
statement 9;  
statement 10;  
```
Suppose there are 10 statements in a Java program and an exception occurs at statement 5; the rest of the code will not be executed, i.e., statements 6 to 10 will not be executed. However, when we perform exception handling, the rest of the statements will be executed. That is why we use exception handling in Java.

## Hierarchy of Java Exception classes
The java.lang.Throwable class is the root class of Java Exception hierarchy inherited by two subclasses: Exception and Error. The hierarchy of Java Exception classes is given below:

![image](https://user-images.githubusercontent.com/84008107/133203706-e13c18b2-07c4-4f66-90d8-b9ea6460e24f.png)

## Types of Java Exceptions
There are mainly two types of exceptions: checked and unchecked. An error is considered as the unchecked exception. However, according to Oracle, there are three types of exceptions namely:
<ul>
  <li>Checked Exception</li>
  <li>Unchecked Exception</li>
  <li>Error</li>
</ul>

## Difference between Checked and Unchecked Exceptions

1) Checked Exception

The classes that directly inherit the Throwable class except RuntimeException and Error are known as checked exceptions. For example, IOException, SQLException, etc. Checked exceptions are checked at compile-time.

2) Unchecked Exception
 
The classes that inherit the RuntimeException are known as unchecked exceptions. For example, ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException, etc. Unchecked exceptions are not checked at compile-time, but they are checked at runtime.

3) Error

Error is irrecoverable. Some example of errors are OutOfMemoryError, VirtualMachineError, AssertionError etc.

## Java Exception Keywords
Java provides five keywords that are used to handle the exception. The following table describes each.

<table>
  <tr><td>Keyword</td>	<td>Description</td></tr>
  <tr><td>try</td>	<td>The "try" keyword is used to specify a block where we should place an exception code. It means we can't use try block alone. The try block must be followed by either catch or finally.</td></tr>
  <tr><td>catch</td>	<td>The "catch" block is used to handle the exception. It must be preceded by try block which means we can't use catch block alone. It can be followed by finally block later.</td></tr>
  <tr><td>finally	</td> <td>The "finally" block is used to execute the necessary code of the program. It is executed whether an exception is handled or not.</td></tr>
  <tr><td>throw</td>	<td>The "throw" keyword is used to throw an exception.</td></tr>
  <tr><td>throws</td>	<td>The "throws" keyword is used to declare exceptions. It specifies that there may occur an exception in the method. It doesn't throw an exception. It is always used with method signature.</td></tr>
</table>

## Java Exception Handling Example
Let's see an example of Java Exception Handling in which we are using a try-catch statement to handle the exception.

```java
public class JavaExceptionExample{  
  public static void main(String args[]){  
   try{  
      //code that may raise exception  
      int data=100/0;  
   }catch(ArithmeticException e){System.out.println(e);}  
   //rest code of the program   
   System.out.println("rest of the code...");  
  }  
}  
```
## Calculator Example
```java
import java.util.Scanner;

public class Calculator
{
	public static void main(String[] args)
	{
		int x=1,y=1,z;
		String str,str1;
		Scanner number = new Scanner(System.in);
			System.out.println("Give me the first integer.");
			str=number.nextLine();
			try
			{
				x=Integer.parseInt(str);
			}
			catch(NumberFormatException e)
			{
				if ("".equals(str))
				{
					System.out.println("No number is given.Setting x as 1.");
				}
				else if (str.length()>0)
				{
					System.out.println("You gave a string.Setting x to 1");
				}
			}
			System.out.println("Give me the second integer.");
			str1=number.nextLine();
				try
				{
					y=Integer.parseInt(str1);
				}
				catch(NumberFormatException e)
				{
					if ("".equals(str1))
					{
						System.out.println("No number is given.Setting y as 1.");
					}
					else if (str1.length()>0)
					{
						System.out.println("You gave a string.Setting y to 1");
					}
				}
			number.close();
			try
			{
			z=(x-7)*y/(x-2);
			System.out.println("The result equals to "+z);
			}
			catch (ArithmeticException e){}
			finally
			{
				if ((x==2) && (y>0))
				{
					System.out.println("Result is -00");
				}
				else if ((x==2)&&(y<0))
				{
					System.out.println("Result is +00");
				}
				else if ((x==2) && (y==0))
				{
					System.out.println("Result is undefined");
				}
			}
	}
}
```
