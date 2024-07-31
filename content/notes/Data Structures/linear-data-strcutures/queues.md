---
title: "Queues"
draft: false
---

### Queues

Queues are a fundamental concept in computer science that follow the First In, First Out (FIFO) principle. Imagine a queue as a line at a checkout counter: the first person to line up is the first one to be served. Similarly, in a queue data structure, the first element added is the first one to be removed. This orderly processing makes queues ideal for tasks where maintaining the sequence of events is crucial.

### Historical Context

The idea of queues has been around since the early days of computing. As computer scientists began developing more complex algorithms and systems, they realized the need for mechanisms to handle data and tasks in a structured manner. By the 1960s, queues had become a formalized concept, playing a crucial role in the development of early operating systems and programming languages. Their ability to manage data flow and tasks efficiently laid the foundation for many modern computing systems.

### Understanding Queues

Think of a queue like a line of people waiting at a bank: new arrivals join at the end, and the person at the front is served first. In the context of computer science, a queue functions similarly. New elements are added to the rear of the queue, while elements are removed from the front. This ensures that elements are processed in the order they arrive.

In Java, you can create a queue using various approaches, like arrays or linked lists. Java also offers built-in support through the `Queue` interface, with implementations like `LinkedList` and `PriorityQueue`. Here's a simple example of how to implement a queue using a linked list:

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class Queue {
    private Node front;
    private Node rear;

    // Initialize the queue
    public Queue() {
        this.front = null;
        this.rear = null;
    }

    // Add a new element to the rear of the queue
    public void enqueue(int data) {
        Node newNode = new Node(data);
        if (rear == null) {
            front = newNode;
            rear = newNode;
        } else {
            rear.next = newNode;
            rear = newNode;
        }
    }

    // Remove the front element from the queue
    public int dequeue() {
        if (front == null) throw new RuntimeException("Queue is empty");
        int data = front.data;
        front = front.next;
        if (front == null) rear = null;
        return data;
    }

    // View the front element without removing it
    public int peek() {
        if (front == null) throw new RuntimeException("Queue is empty");
        return front.data;
    }

    // Check if the queue is empty
    public boolean isEmpty() {
        return front == null;
    }
}

public class Main {
    public static void main(String[] args) {
        Queue queue = new Queue();
        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        System.out.println("Front element is: " + queue.peek()); // Output: Front element is: 10
        System.out.println("Removed element is: " + queue.dequeue()); // Output: Removed element is: 10
        System.out.println("Front element is: " + queue.peek()); // Output: Front element is: 20
    }
}
```

In this example, the `Node` class represents each item in the queue, and the `Queue` class manages operations like adding, removing, and viewing elements. The `main` method shows how to use the queue to handle data.

### Advantages of Queues

Queues offer several benefits, particularly in scenarios where the order of processing is important. The FIFO principle ensures that elements are handled in the exact sequence they arrive, which is essential for many applications. Additionally, both adding and removing elements from a queue can be done quickly (in constant time, O(1)), making queues efficient for real-time processing.

Queues are useful in various fields, such as task scheduling in operating systems, where tasks are managed in the order they are received. They are also crucial in networking, where data packets are managed to ensure they are transmitted and processed correctly.

### Common Operations

Queues support a few key operations:

- **Enqueue:** Add a new element to the rear of the queue.
- **Dequeue:** Remove the element from the front of the queue.
- **Peek:** View the front element without removing it.
- **IsEmpty:** Check if the queue has no elements.

These operations help in managing data efficiently and are used in various applications from task scheduling to data processing.

### Types of Queues

Queues come in several variations, each suited to different needs:

- **Simple Queue:** The basic FIFO queue where elements are added to the rear and removed from the front.
- **Circular Queue:** This type of queue connects the rear to the front, forming a circle. It uses space more efficiently and avoids shifting elements.
- **Priority Queue:** Elements are processed based on their priority. Higher-priority elements are dequeued before lower-priority ones.
- **Double-ended Queue (Deque):** Elements can be added or removed from both ends, offering more flexibility.

Here’s an example of a circular queue in Java:

```java
class CircularQueue {
    private int[] queue;
    private int front;
    private int rear;
    private int size;
    private int capacity;

    // Initialize the circular queue
    public CircularQueue(int capacity) {
        this.capacity = capacity;
        this.queue = new int[capacity];
        this.front = 0;
        this.rear = -1;
        this.size = 0;
    }

    // Add a new element to the rear
    public void enqueue(int data) {
        if (size == capacity) throw new RuntimeException("Queue is full");
        rear = (rear + 1) % capacity;
        queue[rear] = data;
        size++;
    }

    // Remove the front element
    public int dequeue() {
        if (size == 0) throw new RuntimeException("Queue is empty");
        int data = queue[front];
        front = (front + 1) % capacity;
        size--;
        return data;
    }

    // View the front element
    public int peek() {
        if (size == 0) throw new RuntimeException("Queue is empty");
        return queue[front];
    }

    // Check if the queue is empty
    public boolean isEmpty() {
        return size == 0;
    }

    // Check if the queue is full
    public boolean isFull() {
        return size == capacity;
    }
}

public class Main {
    public static void main(String[] args) {
        CircularQueue queue = new CircularQueue(5);
        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        System.out.println("Front element is: " + queue.peek()); // Output: Front element is: 10
        System.out.println("Removed element is: " + queue.dequeue()); // Output: Removed element is: 10
        System.out.println("Front element is: " + queue.peek()); // Output: Front element is: 20
    }
}
```

This code demonstrates how a circular queue operates, efficiently managing space and maintaining the queue's circular structure.

### Practical Uses of Queues

Queues are widely used due to their efficiency and versatility. They are essential in task scheduling and process management, ensuring that tasks are executed in the order they are received. In multimedia applications, queues help buffer data to maintain smooth playback. Additionally, algorithms like breadth-first search (BFS) use queues to explore data structures systematically.

### Visual Representation

To visualize a queue, imagine a line of people at a bus stop: the first person in line boards the bus first, while new arrivals join the end of the line. Here's a simple illustration of a queue:

```
Front
 |
[10] <- Front element
[20]
[30]
 |
Rear
```

In this illustration, the queue has three elements, with the first element (10) at the front and the most recent element (30) at the rear. Elements are removed from the front and added to the rear, following the FIFO principle.