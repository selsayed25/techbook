---
title: "Linked Lists"
draft: false
---

## Linked Lists

Linked lists are a core data structure in computer science, offering a dynamic and flexible way to handle and organize data. Unlike arrays, linked lists don’t need a contiguous block of memory, which means they can grow and shrink more easily. This makes them particularly useful when the size of the data collection is unpredictable or frequently changing.

### A Bit of History

The idea of linked lists has been around since the early days of computing. In the 1950s, as programming languages and computer systems were evolving, researchers sought efficient ways to manage data that could change in size. Allen Newell and his team at RAND Corporation were among the first to introduce linked lists while working on the Information Processing Language (IPL). Since then, linked lists have become fundamental in computer science, serving as the foundation for many other data structures and algorithms.

### What Are Linked Lists?

A linked list is a type of data structure where each element, called a node, contains two parts: the data and a reference (or link) to the next node in the sequence. The first node is known as the head, and the last node, which points to nothing (null), is called the tail. The main advantage of linked lists over arrays is their flexibility. You can easily add or remove elements without worrying about resizing or shifting other elements.

Here’s a basic example of how you might implement a singly linked list in Java:

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    Node head;

    // Method to add a new node at the end of the list
    public void add(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }

    // Method to print all nodes in the list
    public void printList() {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.add(10);
        list.add(20);
        list.add(30);
        list.printList(); // Output: 10 20 30
    }
}
```

In this code, `Node` represents a node in the linked list, and `LinkedList` manages the list, with methods to add nodes and print the list’s contents.

### Why Linked Lists Are Useful

Linked lists come with several advantages:

- **Dynamic Size:** Unlike arrays, linked lists don’t need to have a fixed size. They can grow and shrink as needed, which is useful if you don’t know in advance how many elements you’ll need.

- **Efficient Insertions and Deletions:** Adding or removing nodes can be done quickly, as it only involves updating a few references. This makes linked lists ideal for applications where you need to frequently add or remove elements.

- **No Fragmentation Issues:** Linked lists don’t suffer from memory fragmentation issues like arrays might, as they don’t require contiguous memory allocation.

### Types of Linked Lists

There are several types of linked lists, each with its own unique features:

- **Singly Linked Lists:** Each node points to the next node in the list. This is the simplest form, as shown in the previous example.

- **Doubly Linked Lists:** Each node has two references: one to the next node and one to the previous node. This allows for efficient traversal in both directions but requires more memory. Here’s a basic implementation in Java:

```java
class DoublyNode {
    int data;
    DoublyNode next;
    DoublyNode prev;

    DoublyNode(int data) {
        this.data = data;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
    DoublyNode head;

    // Method to add a new node at the end of the list
    public void add(int data) {
        DoublyNode newNode = new DoublyNode(data);
        if (head == null) {
            head = newNode;
        } else {
            DoublyNode current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
            newNode.prev = current;
        }
    }

    // Method to print all nodes in the list from head to tail
    public void printList() {
        DoublyNode current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
    }

    // Method to print all nodes in the list from tail to head
    public void printReverse() {
        DoublyNode current = head;
        if (current == null) return;
        while (current.next != null) {
            current = current.next;
        }
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.prev;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        DoublyLinkedList list = new DoublyLinkedList();
        list.add(10);
        list.add(20);
        list.add(30);
        list.printList(); // Output: 10 20 30
        System.out.println();
        list.printReverse(); // Output: 30 20 10
    }
}
```

In this example, the `DoublyNode` class represents nodes in a doubly linked list, with methods to add nodes, print the list from head to tail, and print it in reverse.

- **Circular Linked Lists:** In this type, the last node points back to the first node, forming a circle. This is useful for applications where you need to cycle through the list continuously, such as in certain scheduling algorithms.

### Practical Uses of Linked Lists

Linked lists are versatile and used in various applications, from simple data storage to complex algorithms. For instance:

- **Stacks and Queues:** You can implement these data structures using linked lists. For example, a stack can be managed with a singly linked list where nodes are added and removed from the head.

```java
class Stack {
    private Node top;

    // Method to add a new element to the stack
    public void push(int data) {
        Node newNode = new Node(data);
        newNode.next = top;
        top = newNode;
    }

    // Method to remove the top element from the stack
    public int pop() {
        if (top == null) throw new RuntimeException("Stack is empty");
        int data = top.data;
        top = top.next;
        return data;
    }

    // Method to view the top element without removing it
    public int peek() {
        if (top == null) throw new RuntimeException("Stack is empty");
        return top.data;
    }

    // Method to check if the stack is empty
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

In this example, the `Stack` class uses a singly linked list to manage elements with methods to push, pop, peek, and check if the stack is empty.

- **Operating Systems:** Linked lists are also used in memory management systems to track free and allocated memory blocks, helping efficiently allocate and deallocate memory.

### Visualizing Linked Lists

To visualize linked lists, imagine them as a chain of nodes connected by arrows, with each node containing data and a reference to the next one. For a singly linked list, it looks like this:

```
Head
  |
[10] -> [20] -> [30] -> null
```

Here, each node points to the next one, and the last node points to `null`, showing the end of the list.

For a doubly linked list, you also have references to the previous node:

```
Head
  |
null <- [10] <-> [20] <-> [30] -> null
```

In this case, each node points to both the next and previous nodes, allowing traversal in both directions.