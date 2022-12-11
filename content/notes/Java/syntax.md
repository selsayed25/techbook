---
title: "Java Syntax"
draft: false
---

# The Java Syntax

The syntax of Java refers to the set of rules defining how a Java program is written and interpreted.

The syntax is mostly derived from C and C++. Unlike in C++, in Java, there are no global functions or variables, but there are data members which are also regarded as global variables. All code belongs to classes and all values are objects. The only exception is the primitive types, which are not represented by a class instance for performance reasons (though can be automatically converted to objects and vice versa via autoboxing). Some features like operator overloading or unsigned integer types are omitted to simplify the language and to avoid possible programming mistakes.

The Java syntax has been gradually extended in the course of numerous major JDK releases, and now supports capabilities such as generic programming and function literals (called lambda expressions in Java). Since 2017, a new JDK version is released twice a year, with each release bringing incremental improvements to the language.

## Basics

### Identifiers

An identifier is the name of an element in the code. There are certain standard naming conventions to follow when selecting names for elements. Identifiers in Java are case-sensitive.

An identifier can contain:

- Any Unicode character that is a letter (including numeric letters like Roman numerals) or digit.
- Currency sign (such as ¥).
- Connecting punctuation character (such as _).

An identifier cannot:
- Start with a digit.
- Be equal to a reserved keyword, null literal or boolean literal.

### Keywords

[See Java keywords page](keywords.md)

### 