## Java FileOutputStream Class
Java FileOutputStream is an output stream used for writing data to a file.

If you have to write primitive values into a file, use FileOutputStream class. You can write byte-oriented as well as character-oriented data through FileOutputStream class. But, for character-oriented data, it is preferred to use FileWriter than FileOutputStream.

## FileOutputStream class declaration
Let's see the declaration for Java.io.FileOutputStream class:
```java
public class FileOutputStream extends OutputStream  
```

## FileOutputStream class methods
<table>
  <tr><td><b>Method</b></td>	<td><b>Description</b></td></tr>
  <tr><td>protected void finalize()</td><td>	It is used to clean up the connection with the file output stream.</td></tr>
<tr><td>void write(byte[] ary)	</td><td>It is used to write ary.length bytes from the byte array to the file output stream.</td></tr>
<tr><td>void write(byte[] ary, int off, int len)</td><td>	It is used to write len bytes from the byte array starting at offset off to the file output stream.</td></tr>
<tr><td>void write(int b)	</td><td>It is used to write the specified byte to the file output stream.</td></tr>
<tr><td>FileChannel getChannel()	</td><td>It is used to return the file channel object associated with the file output stream.</td></tr>
<tr><td>FileDescriptor getFD()	</td><td>It is used to return the file descriptor associated with the stream.</td></tr>
<tr><td>void close()	</td><td>It is used to closes the file output stream</td></tr>
</table>  

## Example Java FileOutputStream : write byte
```java
import java.io.FileOutputStream;  
public class FileOutputStreamExample {  
    public static void main(String args[]){    
           try{    
             FileOutputStream fout=new FileOutputStream("D:\\testout.txt");    
             fout.write(65);    
             fout.close();    
             System.out.println("success...");    
            }catch(Exception e){System.out.println(e);}    
      }    
}  
```

## Example Java FileOutputStream : write string
```java
import java.io.FileOutputStream;  
public class FileOutputStreamExample {  
    public static void main(String args[]){    
           try{    
             FileOutputStream fout=new FileOutputStream("D:\\testout.txt");    
             String s="Welcome to java.";    
             byte b[]=s.getBytes();//converting string into byte array    
             fout.write(b);    
             fout.close();    
             System.out.println("success...");    
            }catch(Exception e){System.out.println(e);}    
      }    
}  
```
