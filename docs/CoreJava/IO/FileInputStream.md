## Java FileInputStream Class
Java FileInputStream class obtains input bytes from a file. It is used for reading byte-oriented data (streams of raw bytes) such as image data, audio, video etc. You can also read character-stream data. But, for reading streams of characters, it is recommended to use FileReader class.

### Java FileInputStream class declaration
Let's see the declaration for java.io.FileInputStream class:
```java
public class FileInputStream extends InputStream  
```

<b>Java FileInputStream class methods</b>

<table>
  <tr><td><b>Method</b></td><td><b>Description</b></td></tr>
  <tr><td>int available() </td><td>	It is used to return the estimated number of bytes that can be read from the input stream.</td></tr>
<tr><td>int read()	</td><td>It is used to read the byte of data from the input stream.</td></tr>
<tr><td>int read(byte[] b)	</td><td>It is used to read up to b.length bytes of data from the input stream.</td></tr>
<tr><td>int read(byte[] b, int off, int len)	</td><td>It is used to read up to len bytes of data from the input stream.</td></tr>
<tr><td>long skip(long x)	</td><td>It is used to skip over and discards x bytes of data from the input stream.</td></tr>
<tr><td>FileChannel getChannel()	</td><td>It is used to return the unique FileChannel object associated with the file input stream.</td></tr>
<tr><td>FileDescriptor getFD()	</td><td>It is used to return the FileDescriptor object.</td></tr>
<tr><td>protected void finalize()	</td><td>It is used to ensure that the close method is call when there is no more reference to the file input stream.</td></tr>
<tr><td>void close()	</td><td>It is used to closes the stream</td></tr>
</table>  

## Java FileInputStream example 1: read single character
```java
import java.io.FileInputStream;  
public class DataStreamExample {  
     public static void main(String args[]){    
          try{    
            FileInputStream fin=new FileInputStream("D:\\testout.txt");    
            int i=fin.read();  
            System.out.print((char)i);    
  
            fin.close();    
          }catch(Exception e){System.out.println(e);}    
         }    
        }  
```        
Note: Before running the code, a text file named as "testout.txt" is required to be created.

## Java FileInputStream example 2: read all characters
```java
package com.java;  
  
import java.io.FileInputStream;  
public class DataStreamExample {  
     public static void main(String args[]){    
          try{    
            FileInputStream fin=new FileInputStream("D:\\testout.txt");    
            int i=0;    
            while((i=fin.read())!=-1){    
             System.out.print((char)i);    
            }    
            fin.close();    
          }catch(Exception e){System.out.println(e);}    
         }    
        }  
```
