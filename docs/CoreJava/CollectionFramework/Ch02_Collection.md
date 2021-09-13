## Collection

Any group of individual objects which are represented as a single unit is known as collection of objects.eg collection of books,movies etc.

## Framework
A framework is set of classes and interfaces which provides a ready-made architecture.

## Collection Framework
Collection Framework is a java API (Collection of classes and interfaces) which provides an architecture to store and manipulate group of objects(predefined implemenation on the basis of algorithm).

### Collection Framework Hierarchy

All the classes and interfaces of the collection framework are in <b>java.util</b> package. This hierarchy for the collection framework specifically mentioned the class and interface with respect to each type.

![image](https://user-images.githubusercontent.com/84008107/133059867-071ad173-cebc-47f7-96b1-5af84e3043ed.png)

#### Iterable Interface
The Iterable interface is the root interface for all the collection classes because the Collection interface extends the Iterable interface, therefore, all the subclasses of Collection interface also implement the Iterable interface.

The iterable interface contains only one abstract method.

Iterator iterator(): It returns the iterator over the elements of type T.

### Iterator Interface
The iterator interface provides the facility of iterating the elements in a forward direction only.

### Collection Interface
The Collection interface builds the foundation for the Collection framework. The collection interface is one of the interfaces which is implemented by all the Collection framework classes. It provides common methods to implement by all the subclasses of collection interfaces.

### List Interface
List interface is the subtype/child interface of the Collection interface. It stores objects/elements in list type data structure in ordered form and also allowed duplicate values.

Implementation classes for List interface are ArrayList, LinkedList, Vector, and Stack.

For Example: To instantiate List Interface with Implementation classes follow:

```java
List  list1= new ArrayList();  
List  list2 = new LinkedList();  
List  list3 = new Vector();  
List  list4 = new Stack();
```

### ArrayList Class
The ArrayList implements the List interface. It’s having the following features:
<ul>
  <li> ArrayList uses a dynamic array data structure to store objects and elements.</li>
  <li> ArrayList allows duplicate objects and elements.</li>
  <li> ArrayList maintains the insertion order.</li>
  <li> ArrayList is non-synchronized.</li>
  <li> ArrayList elements/objects can be accessed randomly.</li>
</ul>

### LinkedList Class
LinkedList implements the List interface. It’s having the following features:
<ul>
  <li> LinkedList uses a doubly linked list data structure to store elements.</li>
  <li> LinkedList allowed storing the duplicate elements. </li>
  <li> LinkedList maintains the insertion order.</li>
  <li> LinkedList is not synchronized.</li>
  <li> LinkedList manipulation is fast because no shifting is required.</li>
</ul>

### Vector Class ( one of the oldest collection before java 1.2)
Vector Class implements List interface. It’s having the following features:
<ul>
  <li> Vector is similar to the ArrayList class.</li>
  <li> Vector class uses data structure as a dynamic array to store the data elements.</li>
  <li> Vector is synchronized.</li>
  <li> Vector contains many methods that are not the part of Collection Framework.</li>
</ul>

### Stack Class (subclass of Vector Class)
The Stack is the subclass of the Vector class. It’s having the following features:
<ul>
  <li>Stack implements the Vector data structure with the (LIFO)last-in-first-out.</li>
  <li> Stack contains all of the methods of the Vector class.</li>
  <li> Stack also provides its methods like boolean push(), boolean peek(), boolean push(object o), which defines its features.</li>
</ul>  

### Queue Interface

Queue Interface extends the Collection interface. It’s having the following features:
<ul>
  <li> Queue interface maintains the FIFO (first-in-first-out) order.</li>
<li> Queue can be defined as an ordered list that is used to hold the elements which are about to be processed.</li>
<li> Queue interface implemented by the various classes like PriorityQueue, Deque, and ArrayDeque.</li>
</ul>

Queue interface can be instantiated as:
```java
Queue q1 = new PriorityQueue();  
Queue q2 = new ArrayDeque();  
```
### PriorityQueue
The PriorityQueue class implements the Queue interface.
<ul>
  <li>PriorityQueue holds the elements or objects which are to be processed by their priorities.</li>
  <li> PriorityQueue doesn’t allow null values to be stored in the queue.</li>
</ul>

### Deque Interface

Deque stands for the double-ended queue which allows us to perform the operations at both ends.interface extends the Queue interface.
<ul>
  <li> Deque extends the Queue interface.</li>
  <li> Deque allows remove and add the elements from both the side.</li>
</ul>  
```java
  Deque d = new ArrayDeque(); 
```  

### ArrayDeque Class
ArrayDeque class implements the Deque interface.
<ul>
  <li> ArrayDeque facilitates us to use the Deque.</li>
  <li>ArrayDeque allows add or delete the elements from both the ends.</li>
  <li>ArrayDeque is faster than ArrayList and has no capacity restrictions.</li>
</ul>

### Set Interface
Set Interface extends Collection Interface and present in java.util package.
<ul>
  <li>Set doesn’t allow duplicate elements or objects.</li>
  <li>Set store elements in an unordered way.</li>
  <li>Set allows only one null value.</li>
  <li>Set is implemented by HashSet, LinkedHashSet, and TreeSet.</li>
</ul>  
```java
 // We can create an instantiation of Set as below:

Set s1 = new HashSet();  
Set s2 = new LinkedHashSet();  
Set s3 = new TreeSet();
```

### HashSet
HashSet class implements Set Interface. It’s having the following features:
<ul>
  <li>HashSet internally uses data structure like a hash table for storage.</li>
  <li>HashSet uses hashing technique for storage of the elements.</li>
  <li>HashSet always contains unique items.</li>
</ul>

### LinkedHashSet
LinkedHashSet class implements Set Interface. It’s having the following features:
<ul>
  <li>LinkedHashSet store items in LinkedList.</li>
  <li>LinkedHashSet store unique elements.</li>
  <li>LinkedHashSet maintains the insertion order.</li>
  <li>LinkedHashSet allows null elements.</li>
</ul>

### SortedSet Interface
SortedSet Interface extends Set Interface. It’s having the following features:
<ul>
  <li>SortedSet provides a total ordering on its elements.</li>
  <li>SortedSet elements are arranged in the increasing (ascending) order.</li>
  <li>SortedSet provides additional methods that inhibit the natural ordering of the elements.</li>
</ul>
```java
  //The SortedSet can be instantiated as:

SortedSet set = new TreeSet();  
For more detail: Java: SortedSet Interface methods and Examples
```

### TreeSet Class
TreeSet class implements the SortedSet interface.  It’s having the following features:
<ul>
  <li>TreeSet uses a tree data structure for storage.</li>
  <li>TreeSet also contains unique elements.</li>
  <li>TreeSet elements access and retrieval time is quite fast.</li>
  <li>TreeSet elements stored in ascending order.</li>
</ul>

### Map Interface
In the collection framework, a map contains values on the basis of key and value pair. This pair is known as an entry. A map having the following features:
<ul>
  <li> Map contains unique keys.</li>
  <li>Map allows duplicate values.</li>
  <li>Map is useful to search, update or delete elements on the basis of a key.</li>
  <li>Map is the root interface in Map hierarchy for Collection Framework.</li>
  <li>Map interface is extended by SortedMap and implemented by HashMap, LinkedHashMap.</li>
<li>Map implementation classes HashMap and LinkedHashMap allow null keys and values but TreeMap doesn’t allow null key and value.</li>
<li>Map can’t be traversed, for traversing needs to convert into the set using method keySet() or entrySet().</li>
</ul>

### HashMap Class
HashMap class implements Map interface. It’s having following features:
<ul>
  <li> HashMap uses data structure as a Hash Table.</li>
  <li>HashMap store values based on keys.</li>
  <li>HashMap contains unique keys.</li>
  <li>HashMap allows duplicate values.</li>
  <li>HashMap doesn’t maintain order.</li>
  <li>HashMap class allows only one null key and multiple null values.</li>
  <li>HashMap is not synchronized.</li>
  <li>HashMap initial default capacity is 16 elements with a load factor of 0.75.</li>
</ul>

### LinkedHashMap Class
LinkedHashMap class extends the HashMap class. It’s having the following features:
<ul>
  <li> LinkedHashMap contains values based on the key.</li>
  <li> LinkedHashMap contains unique elements.</li>
  <li> LinkedHashMap may have one null key and multiple null values.</li>
  <li>LinkedHashMap is not synchronized.</li>
  <li>LinkedHashMap maintains the insertion order.</li>
  <li>LinkedHashMap default initial capacity is 16 with a load factor of 0.75.</li>
</ul>

### TreeMap Class
TreeMap class implements the SortedMap interface. it’s having the following features:
<ul>
  <li> TreeMap uses data structure as red-black tree.</li>
<li>TreeMap contains values based on the key. It implements the NavigableMap interface and extends AbstractMap class.</li>
  <li>TreeMap contains only unique elements.</li>
  <li>TreeMap doesn’t allow null keys and values.</li>
  <li>TreeMap is not synchronized.</li>
  <li>TreeMap maintains an ascending order.</li>
</ul>

### HashTable Class
Hashtable class implements a Map interface and extends Dictionary class to store key and values as pairs. It’s having the following features:
<ul>
<li>HashTable store values as an array of the list where each list is known as a bucket of the node(key and value pair).</li>
  <li>HashTable class is in java.util package.</li>
  <li>Hashtable contains unique elements.</li>
  <li>Hashtable doesn’t allow null key or value.</li>
  <li>Hashtable is synchronized.</li>
  <li>Hashtable initial default capacity is 11 whereas the load factor is 0.75.</li>
</ul>  
