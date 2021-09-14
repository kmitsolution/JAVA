## Properties class in Java
The properties object contains key and value pair both as a string. The java.util.Properties class is the subclass of Hashtable.

It can be used to get property value based on the property key. The Properties class provides methods to get data from the properties file and store data into the properties file. Moreover, it can be used to get the properties of a system.

### An Advantage of the properties file
Recompilation is not required if the information is changed from a properties file: If any information is changed from the properties file, you don't need to recompile the java class. It is used to store information which is to be changed frequently.

## Constructors of Properties class
<table>
  <tr><td><b>Method</b></td><td><b>	Description</b></td></tr>
<tr><td>Properties() </td><td>	It creates an empty property list with no default values.</td></tr>
<tr><td>Properties(Properties defaults)	</td><td>It creates an empty property list with the specified defaults.</td></tr>
</table>
  
  <b>Methods of Properties class</b>
The commonly used methods of Properties class are given below
<table>
<tr><td><b>Method</b></td><td><b>	Description</b></td></tr>
<tr><td>public void load(Reader r)	</td><td>It loads data from the Reader object.</td></tr>
<tr><td>public void load(InputStream is) </td><td>	It loads data from the InputStream object</td></tr>
<tr><td>public void loadFromXML(InputStream in)	</td><td>It is used to load all of the properties represented by the XML document on the specified input stream into this properties table.</td></tr>
<tr><td>public String getProperty(String key) </td><td>	It returns value based on the key.</td></tr>
<tr><td>public String getProperty(String key, String defaultValue)	</td><td>It searches for the property with the specified key.</td></tr>
<tr><td>public void setProperty(String key, String value)	</td><td>It calls the put method of Hashtable.</td></tr>
<tr><td>public void list(PrintStream out)	</td><td>It is used to print the property list out to the specified output stream.</td></tr>
<tr><td>public void list(PrintWriter out))	</td><td>It is used to print the property list out to the specified output stream.</td></tr>
<tr><td>public Enumeration<?> propertyNames()) </td><td>	It returns an enumeration of all the keys from the property list.</td></tr>
<tr><td>public Set<String> stringPropertyNames()	</td><td>It returns a set of keys in from property list where the key and its corresponding value are strings.</td></tr>
<tr><td>public void store(Writer w, String comment)	</td><td>It writes the properties in the writer object.</td></tr>
<tr><td>public void store(OutputStream os, String comment)	</td><td>It writes the properties in the OutputStream object.</td></tr>
<tr><td>public void storeToXML(OutputStream os, String comment)	</td><td>It writes the properties in the writer object for generating XML document.</td></tr>
<tr><td>public void storeToXML(Writer w, String comment, String encoding)	</td><td>It writes the properties in the writer object for generating XML document with the specified encoding.</td></tr>
</table>

## Example of Properties class to get information from the properties file

To get information from the properties file, create the properties file first.

db.properties
```
user=system  
password=oracle  
```
Now, let's create the java class to read the data from the properties file.
```java
Test.java
import java.util.*;  
import java.io.*;  
public class Test {  
public static void main(String[] args)throws Exception{  
    FileReader reader=new FileReader("db.properties");  
      
    Properties p=new Properties();  
    p.load(reader);  
      
    System.out.println(p.getProperty("user"));  
    System.out.println(p.getProperty("password"));  
}  
}  
```

## Example of Properties class to get all the system properties

By System.getProperties() method we can get all the properties of the system. Let's create the class that gets information from the system properties.

```java
import java.util.*;  
import java.io.*;  
public class Test {  
public static void main(String[] args)throws Exception{  
  
Properties p=System.getProperties();  
Set set=p.entrySet();  
  
Iterator itr=set.iterator();  
while(itr.hasNext()){  
Map.Entry entry=(Map.Entry)itr.next();  
System.out.println(entry.getKey()+" = "+entry.getValue());  
}  
  
}  
}  
```

## Example of Properties class to create the properties file

```java
import java.util.*;  
import java.io.*;  
public class Test {  
public static void main(String[] args)throws Exception{  
  
Properties p=new Properties();  
p.setProperty("name","Sonoo Jaiswal");  
p.setProperty("email","sonoojaiswal@java.com");  
  
p.store(new FileWriter("info.properties"),"Java Properties Example");  
  
}  
}  
```

Let's see the generated properties file.
```
info.properties
#Javatpoint Properties Example  
#Thu Oct 03 22:35:53 IST 2013  
email=sonoojaiswal@javatcom  
name=Sonoo Jaiswal  
```
