---
title: "Stacks"
draft: false
---

## Stacks

Stacks are a core concept in computer science, known for their Last In, First Out (LIFO) principle. This means that the most recent item added to the stack is the first one to be removed. Think of a stack like a stack of plates: you add new plates to the top and only take plates off from the top. This simple yet powerful structure is used in many algorithms and applications, thanks to its efficiency and straightforward nature.

### Historical Background

The idea of stacks dates back to the early days of computing. In the 1950s, the concept of a push-down stack was formally introduced by computer scientist Peter J. P. de Jong. Early computer scientists needed a way to manage function calls, memory, and other tasks that required organized data access. Stacks played a crucial role in the development of programming languages and systems, laying the groundwork for how we handle function calls, recursion, and even expression evaluation today.

### What Are Stacks?

Imagine a stack of books where you can only add or remove books from the top. This is how stacks work in computer science: new items are added to the top, and the top item is the first one to be removed. This LIFO principle ensures that the most recent addition is always the first to be accessed or removed.

In Java, stacks can be implemented using various methods. For simplicity, let's look at how you might implement a stack using a linked list:

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class Stack {
    private Node top;

    // Constructor to initialize the stack
    public Stack() {
        this.top = null;
    }

    // Add a new element to the top of the stack
    public void push(int data) {
        Node newNode = new Node(data);
        newNode.next = top;
        top = newNode;
    }

    // Remove the top element from the stack
    public int pop() {
        if (top == null) throw new RuntimeException("Stack is empty");
        int data = top.data;
        top = top.next;
        return data;
    }

    // View the top element without removing it
    public int peek() {
        if (top == null) throw new RuntimeException("Stack is empty");
        return top.data;
    }

    // Check if the stack is empty
    public boolean isEmpty() {
        return top == null;
    }
}

public class Main {
    public static void main(String[] args) {
        Stack stack = new Stack();
        stack.push(10);
        stack.push(20);
        stack.push(30);
        System.out.println("Top element is: " + stack.peek()); // Output: Top element is: 30
        System.out.println("Removed element is: " + stack.pop()); // Output: Removed element is: 30
        System.out.println("Top element is: " + stack.peek()); // Output: Top element is: 20
    }
}
```

In this example, the `Node` class represents each item in the stack, and the `Stack` class manages the stack operations like adding (push) and removing (pop) items. The `peek` method allows you to look at the top item without removing it, and `isEmpty` checks if the stack is empty.

### Why Use Stacks?

Stacks are valuable for several reasons. Their simplicity is a major advantage: the LIFO principle is easy to grasp and implement. Operations like adding (push) and removing (pop) items are performed in constant time, O(1), meaning they're quick and efficient regardless of the stack's size.

Stacks are crucial for managing function calls and recursion. When a function is called, its current state, including local variables and return address, is pushed onto the stack. Once the function completes, its state is popped off, and execution resumes from where it left off. This mechanism is essential for handling recursive algorithms, where each call creates a new layer in the stack.

Stacks also play a role in evaluating expressions and parsing syntax. For instance, while infix notation (like `3 + 4`) is common in programming, postfix notation (like `3 4 +`) is used in some algorithms and compiler designs. Stacks help convert and evaluate these expressions efficiently.

### Basic Operations

Stacks support a few key operations:

- **Push:** Adds a new element to the top of the stack.
- **Pop:** Removes the top element from the stack.
- **Peek:** Views the top element without removing it.
- **IsEmpty:** Checks if the stack is empty.

These operations are fundamental for working with stacks and are used in various applications, from managing function calls to parsing expressions.

### Real-World Uses

Stacks are versatile and find applications in many areas. For example, function call management relies on a call stack to track active functions and their local variables. Each function call pushes a new frame onto the stack, and when the function returns, the frame is popped off.

Stacks are also used in undo mechanisms in software. Applications like text editors and graphic design tools often use stacks to keep track of actions. Each action is pushed onto an undo stack, and when you undo an action, it’s popped from the stack to reverse the effect. Similarly, redo stacks manage actions that have been undone.

In algorithms, stacks are used in depth-first search (DFS) for exploring graph structures. A stack keeps track of vertices to be explored, allowing the algorithm to dive deep along each branch before backtracking.

### Visualizing Stacks

Think of a stack of plates where you can only add or remove plates from the top. The stack grows upward as new plates are added and shrinks downward as plates are removed. 

Here's a simple illustration of a stack with three elements:

```
Top
 |
[30] <- Top element
[20]
[10]
 |
Bottom
```

In this illustration, the most recent element (30) is at the top, and the earliest added element (10) is at the bottom. Elements are added and removed from the top, following the LIFO principle.