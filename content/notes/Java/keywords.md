---
title: "Java Keywords"
draft: false
---

In the Java programming language, a keyword is any one of 67 reserved words that have a predefined meaning in the language. Because of this, programmers cannot use keywords in some contexts, such as names for variables, methods, classes, or as any other identifier. Of these 67 keywords, 16 of them are only contextually reserved, and can sometimes be used as an identifier, unlike standard reserved words. Due to their special functions in the language, most integrated development environments for Java use syntax highlighting to display keywords in a different color for easy identification.

## The long list of Java keywords

### `abstract`

A method with no definition must be declared as abstract and the class containing it must be declared as abstract. Abstract classes cannot be instantiated. Abstract methods must be implemented in the sub classes. The abstract keyword cannot be used with variables or constructors. Note that an abstract class isn't required to have an abstract method at all.

```java
public abstract class Athlete {
    ...
}
```

### `assert`

Assert describes a predicate (a true–false statement) placed in a Java program to indicate that the developer thinks that the predicate is always true at that place. If an assertion evaluates to false at run-time, an assertion failure results, which typically causes execution to abort. Assertions are disabled at runtime by default, but can be enabled through a command-line option or programmatically through a method on the class loader.

### `boolean`

Defines a boolean variable for the values "true" or "false" only. By default, the value of boolean primitive type is false. This keyword is also used to declare that a method returns a value of the primitive type `boolean`.

### `break`

Used to end the execution in the current loop body.

### `byte`

The `byte` keyword is used to declare a field that can hold an 8-bit signed two's complement integer. This keyword is also used to declare that a method returns a value of the primitive type `byte`.

### `case`

A statement in the `switch` block can be labeled with one or more `case` or `default` labels. The `switch` statement evaluates its expression, then executes all statements that follow the matching `case` label; see `switch`.

### `catch`

Used in conjunction with a `try` block and an optional `finally` block. The statements in the `catch` block specify what to do if a specific type of exception is thrown by the `try` block.

### `char`

Defines a character variable capable of holding any character of the java source file's character set.

### `class`

A type that defines the implementation of a particular kind of object. A class definition defines instance and class fields, methods, and inner classes as well as specifying the interfaces the class implements and the immediate superclass of the class. If the superclass is not explicitly specified, the superclass is implicitly `Object`. The class keyword can also be used in the form `Class.class` to get a Class object without needing an instance of that class. For example, `String.class` can be used instead of doing `new String().getClass()`.

### `const`

Unused but reserved.

### `continue`

Used to resume program execution at the end of the current loop body. If followed by a label, `continue` resumes execution at the end of the enclosing labeled loop body.

### `default`

The `default` keyword can optionally be used in a switch statement to label a block of statements to be executed if no `case` matches the specified value; see *`switch`*. Alternatively, the default keyword can also be used to declare default values in a Java annotation. From Java 8 onwards, the default keyword can be used to allow an interface to provide an implementation of a method.

### `do`

The `do` keyword is used in conjunction with `while` to create a do-while loop, which executes a block of statements associated with the loop and then tests a boolean expression associated with the `while`. If the expression evaluates to `true`, the block is executed again; this continues until the expression evaluates to `false`.

### `double`

The `double` keyword is used to declare a variable that can hold a 64-bit double precision IEEE 754 floating-point number. This keyword is also used to declare that a method returns a value of the primitive type `double`.

### `else`

The `else` keyword is used in conjunction with `if` to create an if-else statement, which tests a boolean expression; if the expression evaluates to `true`, the block of statements associated with the `if` are evaluated; if it evaluates to `false`, the block of statements associated with the `else` are evaluated.

### `enum`

A Java keyword used to declare an enumerated type. Enumerations extend the base class `Enum`.

### `extends`

Used in a class declaration to specify the superclass; used in an interface declaration to specify one or more superinterfaces. Class X extends class Y to add functionality, either by adding fields or methods to class Y, or by overriding methods of class Y. An interface Z extends one or more interfaces by adding methods. Class X is said to be a subclass of class Y; Interface Z is said to be a subinterface of the interfaces it extends.
Also used to specify an upper bound on a type parameter in Generics.

### `final`

Define an entity once that cannot be changed nor derived from later. More specifically: a final class cannot be subclassed, a final method cannot be overridden, and a final variable can occur at most once as a left-hand expression on an executed command. All methods in a final class are implicitly `final`.

### `finally`

Used to define a block of statements for a block defined previously by the `try` keyword. The `finally` block is executed after execution exits the `try` block and any associated `catch` clauses regardless of whether an exception was thrown or caught, or execution left method in the middle of the `try` or `catch` blocks using the `return` keyword.

### `float`

The `float` keyword is used to declare a variable that can hold a 32-bit single precision IEEE 754 floating-point number. This keyword is also used to declare that a method returns a value of the primitive type `float`.

### `for`

The `for` statement provides a compact way to iterate over a range of values. Programmers often refer to it as the "for loop" because of the way in which it repeatedly loops until a particular condition is satisfied. The general form of the `for` statement can be expressed as follows:

```java
for (initialization; termination; increment) {
    statement(s)
}
```