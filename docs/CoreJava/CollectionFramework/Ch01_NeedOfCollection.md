# Collection Framework in java
![image](https://user-images.githubusercontent.com/84008107/133050386-35b1152e-d971-4fdf-8e10-affd764434f5.png)

## Array 

A Java array is a type of object in Java, known as a container object. It is used to contain objects of a single type as a part of a single set. The data type of all the array elements in Java is the say, be it textual, integral, or decimal. To create a Java array, the programmer must first know what the length of the array is going to be. The length of the array in Java cannot be increased after the array has been created.

### Limitation of Array
<ul>
  <li> Static and fix number of elements </li>
  <li> Collection of Similar type elements </li>
  <li> Not any readymade algorithm to solve searcning,sorting etc problems </li>
</ul>

### Let's see below example of Array, In this case count array is of 3 so you cannot store more than 3 elements in count array.

```java
package com.java.array;
public class arraylimitationEx1 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int[] count= new int[3]; // an integer array get created for 3 elements
		count[0]=1;
		count[1]=2;
		count[2]=3;
		count[3]=4; //It is an error here because size of count array is 3
    count[0]="Testing";//Error because count is integer type
	}
	

}

```

### Example 2
```java
package com.java.array;
public class arraylimitationEx1 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Emp[] emps = new Emp[5]; // 5 employees data 
		HR[] hrs = new HR[5]; //5 HR data.
		
	}
	

}
class Emp{
	
}
class HR {
	
}
```
