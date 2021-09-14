## Java I/O
Java I/O (Input and Output) is used to process the input and produce the output.

Java uses the concept of a stream to make I/O operation fast. The java.io package contains all the classes required for input and output operations.

We can perform file handling in Java by Java I/O API.

## Stream
A stream is a sequence of data. In Java, a stream is composed of bytes. It's called a stream because it is like a stream of water that continues to flow.

In Java, 3 streams are created for us automatically. All these streams are attached with the console.

1) System.out: standard output stream

2) System.in: standard input stream

3) System.err: standard error stream

Let's see the code to print output and an error message to the console.
```java
System.out.println("simple message");  
System.err.println("error message");  
```
Let's see the code to get input from console.

```java
int i=System.in.read();//returns ASCII code of 1st character  
System.out.println((char)i);//will print the character  
```

## OutputStream
Java application uses an output stream to write data to a destination; it may be a file, an array, peripheral device or socket.

## InputStream
Java application uses an input stream to read data from a source; it may be a file, an array, peripheral device or socket.

Let's understand the working of Java OutputStream and InputStream by the figure given below.

![image](https://user-images.githubusercontent.com/84008107/133209771-9e20abd5-b21b-448d-82c9-a91a0784065a.png)

## OutputStream class
OutputStream class is an abstract class. It is the superclass of all classes representing an output stream of bytes. An output stream accepts output bytes and sends them to some sink.

Useful methods of OutputStream


<table>
  <tr><td><b>Method	</b> </td><td><b>Description</b></td></tr>
  <tr><td>1) public void write(int)throws IOException </td><td>	is used to write a byte to the current output stream.</td></tr>
<tr><td>2) public void write(byte[])throws IOException</td><td>	is used to write an array of byte to the current output stream.</td></tr>
<tr><td>3) public void flush()throws IOException	</td><td>flushes the current output stream.</td></tr>
<tr><td>4) public void close()throws IOException</td><td>	is used to close the current output stream.</td></tr>
</table>

## OutputStream Hierarchy

![image](https://user-images.githubusercontent.com/84008107/133210701-c2fe84cc-7429-453d-8e97-41ad62f96727.png)

## InputStream class
InputStream class is an abstract class. It is the superclass of all classes representing an input stream of bytes.

Useful methods of InputStream
<table>
<tr><td><b>Method	</b> </td><td><b>Description</b></td></tr>
<tr><td>1) public abstract int read()throws IOException	</td><td>reads the next byte of data from the input stream. It returns -1 at the end of the file.</td></tr>
<tr><td>2) public int available()throws IOException	</td><td>returns an estimate of the number of bytes that can be read from the current input stream.</td></tr>
<tr><td>3) public void close()throws IOException	</td><td>is used to close the current input stream.</td></tr>
  </table>

## InputStream Hierarchy

![image](https://user-images.githubusercontent.com/84008107/133211236-6af2f222-a615-410a-87cf-08e3c8ab5b54.png)
