## Example 1 :- Stack Creation
```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        // Creating a Stack
        Stack<String> stackOfCards = new Stack<>();

        // Pushing new items to the Stack
        stackOfCards.push("Jack");
        stackOfCards.push("Queen");
        stackOfCards.push("King");
        stackOfCards.push("Ace");

        System.out.println("Stack => " + stackOfCards);
        System.out.println();

        // Popping items from the Stack
        String cardAtTop = stackOfCards.pop();  // Throws EmptyStackException if the stack is empty
        System.out.println("Stack.pop() => " + cardAtTop);
        System.out.println("Current Stack => " + stackOfCards);
        System.out.println();

        // Get the item at the top of the stack without removing it
        cardAtTop = stackOfCards.peek();
        System.out.println("Stack.peek() => " + cardAtTop);
        System.out.println("Current Stack => " + stackOfCards);

    }
}

```
## Example 2 :- Stack Iteration

```java
import java.util.Iterator;
import java.util.ListIterator;
import java.util.Stack;

public class IterateOverStackExample {
    public static void main(String[] args) {
        Stack<String> stackOfPlates = new Stack<>();

        stackOfPlates.add("Plate 1");
        stackOfPlates.add("Plate 2");
        stackOfPlates.add("Plate 3");
        stackOfPlates.add("Plate 4");

        System.out.println("=== Iterate over a Stack using Java 8 forEach() method ===");
        stackOfPlates.forEach(plate -> {
            System.out.println(plate);
        });

        System.out.println("\n=== Iterate over a Stack using iterator() ===");
        Iterator<String> platesIterator = stackOfPlates.iterator();
        while (platesIterator.hasNext()) {
            String plate = platesIterator.next();
            System.out.println(plate);
        }

        System.out.println("\n=== Iterate over a Stack using iterator() and Java 8 forEachRemaining() method ===");
        platesIterator = stackOfPlates.iterator();
        while (platesIterator.hasNext()) {
            String plate = platesIterator.next();
            System.out.println(plate);
        }


        System.out.println("\n=== Iterate over a Stack from TOP to BOTTOM using listIterator() ===");
        // ListIterator allows you to traverse in both forward and backward directions.
        // We'll start from the top of the stack and traverse backwards.
        ListIterator<String> platesListIterator = stackOfPlates.listIterator(stackOfPlates.size());
        while (platesListIterator.hasPrevious()) {
            String plate = platesListIterator.previous();
            System.out.println(plate);
        }
    }
}
```
## Example 4:- Stack size search 
```java
import java.util.Stack;

public class StackSizeSearchExample {
    public static void main(String[] args) {
        Stack<String> stackOfCards = new Stack<>();

        stackOfCards.push("Jack");
        stackOfCards.push("Queen");
        stackOfCards.push("King");
        stackOfCards.push("Ace");

        System.out.println("Stack : " + stackOfCards);

        // Check if the Stack is empty
        System.out.println("Is Stack empty? : " + stackOfCards.isEmpty());

        // Find the size of Stack
        System.out.println("Size of Stack : " + stackOfCards.size());

        // Search for an element
        // The search() method returns the 1-based position of the element from the top of the stack
        // It returns -1 if the element was not found in the stack
        int position = stackOfCards.search("Queen");

        if(position != -1) {
            System.out.println("Found the element \"Queen\" at position : " + position);
        } else {
            System.out.println("Element not found");
        }

    }
}
```
