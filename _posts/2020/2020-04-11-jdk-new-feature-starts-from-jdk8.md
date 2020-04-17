---
date: 2020-04-01T04:00:00.000+00:00
categories:
- jdk
title: JDK New Features Summary

---
## JDK14

* Switch Expressions

```java
var log = switch (event) {
    case PLAY -> "User has triggered the play button";
    case STOP, PAUSE -> "User needs a break";
    default -> {
        String message = event.toString();
        LocalDateTime now = LocalDateTime.now();
        yield "Unknown event " + message + 
              " logged on " + now;
    }
};
```

* Text Block (Preview)
* Pattern Matching for `instanceof` (Preview)

```java
if (obj instanceof Group) {
  Group group = (Group) obj;

  // use group specific methods
  var entries = group.getEntries();
}
```
The above code can be refactored as the following code using the preview feature.
```java
if (obj instanceof Group group) {
  var entries = group.getEntries();
}
```

* JEP 359 Records (Preview)

Consider a simple domain class, BankTransaction, that models a transaction with three fields: a date, an amount, and a description. You need to worry about multiple components when you declare the class:
1. The constructor
2. Getter methods
3. toString()
4. hashCode() and equals()

```java
public class BankTransaction {
    private final LocalDate date;
    private final double amount;
    private final String description;


    public BankTransaction(final LocalDate date, 
                           final double amount, 
                           final String description) {
        this.date = date;
        this.amount = amount;
        this.description = description;
    }

    public LocalDate date() {
        return date;
    }

    public double amount() {
        return amount;
    }

    public String description() {
        return description;
    }

    @Override
    public String toString() {
        return "BankTransaction{" +
                "date=" + date +
                ", amount=" + amount +
                ", description='" + description + '\'' +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        BankTransaction that = (BankTransaction) o;
        return Double.compare(that.amount, amount) == 0 &&
                date.equals(that.date) &&
                description.equals(that.description);
    }

    @Override
    public int hashCode() {
        return Objects.hash(date, amount, description);
    }
}
```

Java 14 provides a way to remove the verbosity and make the intent clear that all you want is a class that only aggregates data together with implementations of the equals, hashCode, and toString methods. You can refactor BankTransaction as follows:

```java
public record BankTransaction(LocalDate date,
                              double amount,
                              String description) {}
```

With a record, you “automatically” get the implementations of equals, hashCode, and toString in addition to the constructor and getters.

* Helpful NullPointerExceptions

> [https://blogs.oracle.com/javamagazine/java-14-arrives-with-a-host-of-new-features](https://blogs.oracle.com/javamagazine/java-14-arrives-with-a-host-of-new-features)
> [https://www.oracle.com/technetwork/java/javase/14all-relnotes-5809668.html#NewFeature](https://www.oracle.com/technetwork/java/javase/14all-relnotes-5809668.html#NewFeature "https://www.oracle.com/technetwork/java/javase/14all-relnotes-5809668.html#NewFeature")

## JDK13

* JEP 354 Switch Expressions (Preview)

```java
String formatted = 
    switch (obj) {
        case Integer i -> String.format("int %d", i)
        case Byte b    -> String.format("byte %d", b);
        case Long l    -> String.format("long %d", l); 
        case Double d  -> String.format("double %f", d); 
        case String s  -> String.format("String %s", s); 
        default        -> obj.toString();
    };
```

* JEP 355 Text Blocks (Preview)

> [https://www.oracle.com/technetwork/java/13-relnote-issues-5460548.html#NewFeature](https://www.oracle.com/technetwork/java/13-relnote-issues-5460548.html#NewFeature "https://www.oracle.com/technetwork/java/13-relnote-issues-5460548.html#NewFeature")

## JDK12

* Support for Unicode 11
* POSIX_SPAWN Option on Linux
* JEP 334 JVM Constants API
* JEP 325 Switch Expressions (Preview)
* Java Strings New Methods
* JEP 305: Pattern Matching for instanceof (Preview)

> [https://www.journaldev.com/28666/java-12-features](https://www.journaldev.com/28666/java-12-features "https://www.journaldev.com/28666/java-12-features")

## JDK11

* New string methods: isBlank
* New file methods
* Pattern recognizing methods
* Epsilon Garbage Collector
* Removed the Java EE and CORBA modules
* Removal of thread functions: stop(Throwable obj) and destroy()
* Optional.isEmpty()
* Local-Variable syntax for Lambda parameters

> [https://www.geeksforgeeks.org/java-11-features-and-comparison/](https://www.geeksforgeeks.org/java-11-features-and-comparison/ "https://www.geeksforgeeks.org/java-11-features-and-comparison/")

## JDK10

* Local variable type inference
* Unmodifiable collections. copyOf etc.
* Container awareness

  > -XX:-UseContainerSupport
  >
  > -XX:ActiveProcessorCount=count
  >
  > -XX:InitialRAMPercentage
  >
  > -XX:MaxRAMPercentage
  >
  > -XX:MinRAMPercentage

> [https://www.baeldung.com/java-10-overview](https://www.baeldung.com/java-10-overview "https://www.baeldung.com/java-10-overview")

## JDK9

* Java module system – Jigsaw Project
* New HTTP Client
* Process API
* Try-With-Resources
* Diamond operator extension
* Interface private method
* Jshell

> [https://www.baeldung.com/new-java-9](https://www.baeldung.com/new-java-9 "https://www.baeldung.com/new-java-9")

## JDK8

* Lambda expressions
* Default method in interface
* Method reference
* Repeating Annotations provide the ability to apply the same annotation type more than once to the same declaration or type use
* Type Annotations provide the ability to apply an annotation anywhere a type is used, not just on a declaration. Used with a pluggable type system, this feature enables improved type checking of your code
* Stream integration into Collections API

> [https://www.oracle.com/technetwork/java/javase/8-whats-new-2157071.html](https://www.oracle.com/technetwork/java/javase/8-whats-new-2157071.html "https://www.oracle.com/technetwork/java/javase/8-whats-new-2157071.html")