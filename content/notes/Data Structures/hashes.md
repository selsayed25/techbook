---
title: "Hashes"
draft: false
---

# Understanding Hashes

Hashes are a key concept in computer science, especially when it comes to handling data efficiently and securely. At their core, hashes turn data of any size into a fixed-size value. This makes it easier to store, retrieve, and verify data quickly. You’ll find hashing used in things like hash tables, cryptographic operations, and data integrity checks.

## A Bit of History

Hashing isn’t a new idea. Its roots stretch back to the early days of computing. The concept took shape in the 1950s when scientists started developing hash tables—a clever way to make data retrieval faster. Hans Peter Luhn, a computer scientist, played a significant role in this by introducing hash tables in 1953. His work laid the foundation for how we manage data today.

The 1970s and 80s saw a leap forward with cryptographic hash functions. These are specialized hashes designed to keep data secure. Ronald Rivest's MD5, introduced in 1991, was one of the first widely-used cryptographic hash functions. While MD5 was great for a time, vulnerabilities eventually led to the creation of more secure options like SHA-1 and SHA-2.

## How Hash Functions and Hash Tables Work

### Hash Functions

Think of a hash function as a mathematical recipe that turns an input (like a string or number) into a fixed-size output, called a hash value. Ideally, this output should be unique for each unique input, though sometimes different inputs can produce the same hash (a collision). A good hash function spreads out the hash values evenly to avoid too many collisions.

In simple terms, if you hash the word "hello," you might get a value like `5d41402abc4b2a76b9719d911017c592`.

A good hash function should:

- **Always Produce the Same Output:** For the same input, the result should be predictable.
- **Distribute Values Evenly:** Hash values should be spread out to minimize collisions.
- **Be Fast:** It should compute quickly, even with large inputs.
- **Be Hard to Reverse:** Given a hash value, it should be tough to figure out the original input.
- **Be Collision-Resistant:** It should be hard to find two different inputs that hash to the same value.

### Hash Tables

Hash tables use hash functions to organize and access data efficiently. Imagine a hash table as an array where each slot is determined by the hash function. This allows for quick storage and retrieval of data. 

Here’s how it works:

- **Insertion:** Compute the hash value for the key and store the data in the corresponding slot.
- **Search:** Use the hash value to find and retrieve the data.
- **Deletion:** Compute the hash value to locate and remove the data.

Handling collisions—when multiple keys hash to the same slot—is one challenge with hash tables. There are different methods to handle this, like:

- **Chaining:** Store colliding items in a linked list at the same slot.
- **Open Addressing:** Look for another slot using a probing technique (like linear or quadratic probing).

## Java Example: Simple Hash Table

Here's a basic example of a hash table in Java, using chaining to handle collisions:

```java
import java.util.LinkedList;

public class HashTable<K, V> {
    private static final int INITIAL_CAPACITY = 16;
    private LinkedList<Entry<K, V>>[] table;

    private static class Entry<K, V> {
        K key;
        V value;
        Entry<K, V> next;

        Entry(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }

    public HashTable() {
        table = new LinkedList[INITIAL_CAPACITY];
        for (int i = 0; i < INITIAL_CAPACITY; i++) {
            table[i] = new LinkedList<>();
        }
    }

    private int hash(K key) {
        return key.hashCode() % table.length;
    }

    public void put(K key, V value) {
        int index = hash(key);
        LinkedList<Entry<K, V>> bucket = table[index];
        for (Entry<K, V> entry : bucket) {
            if (entry.key.equals(key)) {
                entry.value = value;
                return;
            }
        }
        bucket.add(new Entry<>(key, value));
    }

    public V get(K key) {
        int index = hash(key);
        LinkedList<Entry<K, V>> bucket = table[index];
        for (Entry<K, V> entry : bucket) {
            if (entry.key.equals(key)) {
                return entry.value;
            }
        }
        return null;
    }

    public void remove(K key) {
        int index = hash(key);
        LinkedList<Entry<K, V>> bucket = table[index];
        Entry<K, V> previous = null;
        for (Entry<K, V> entry : bucket) {
            if (entry.key.equals(key)) {
                if (previous == null) {
                    bucket.remove(entry);
                } else {
                    previous.next = entry.next;
                }
                return;
            }
            previous = entry;
        }
    }

    public static void main(String[] args) {
        HashTable<String, Integer> hashTable = new HashTable<>();
        hashTable.put("Alice", 30);
        hashTable.put("Bob", 25);
        hashTable.put("Charlie", 35);

        System.out.println("Alice's age: " + hashTable.get("Alice"));
        System.out.println("Bob's age: " + hashTable.get("Bob"));
        hashTable.remove("Bob");
        System.out.println("Bob's age after removal: " + hashTable.get("Bob"));
    }
}
```

This example demonstrates how to create a hash table in Java using chaining to handle collisions. The `put` method adds items, `get` retrieves them, and `remove` deletes them.

## Cryptographic Hash Functions

Cryptographic hash functions are a special type of hash function used for security. They need to meet strict requirements to ensure data integrity and authenticity.

A good cryptographic hash function should:

- **Resist Reversal:** It should be hard to reverse-engineer the original input from the hash value.
- **Prevent Second Pre-image Attacks:** Given an input and its hash, it should be tough to find another input with the same hash.
- **Be Collision-Resistant:** It should be difficult to find two different inputs that produce the same hash value.

Common cryptographic hash functions include:

- **MD5:** Once popular, but now considered insecure.
- **SHA-1:** Also considered weak due to advances in cryptanalysis.
- **SHA-2:** Includes various versions (like SHA-256) and is currently secure.
- **SHA-3:** The latest standard, offering improved security.

## Java Example: Cryptographic Hash Function

Here's how to compute a SHA-256 hash in Java:

```java
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class HashExample {
    public static void main(String[] args) {
        String input = "Hello, world!";
        try {
            MessageDigest md = MessageDigest.getInstance("SHA-256");
            byte[] hashBytes = md.digest(input.getBytes());
            StringBuilder hexString = new StringBuilder();
            for (byte b : hashBytes) {
                String hex = Integer.toHexString(0xff & b);
                if (hex.length() == 1) {
                    hexString.append('0');
                }
                hexString.append(hex);
            }
            System.out.println("SHA-256 hash: " + hexString.toString());
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
        }
    }
}
```

This code uses Java’s `MessageDigest` to compute a SHA-256 hash of a string. It converts the resulting bytes into a readable hexadecimal format.

## The Math Behind Hashing

Hash functions use mathematical principles like modular arithmetic to map data to fixed-size values. For example, a simple hash function might use a modulus operation:

{{< katex >}}h(k) = k \mod m{{< /katex >}}

where {{< katex >}}k{{< /katex >}} is the input and {{< katex >}}m{{< /katex >}} is the hash table size. This keeps the hash value within the bounds of the hash table’s indices.

Understanding the probability of collisions in hash functions can also be enlightening. The Birthday Paradox, for instance, shows that collisions become more likely as the number of items in the hash table grows.