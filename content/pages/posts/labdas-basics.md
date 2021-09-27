---
title: Java 8 Lambdas
excerpt: >-
  Starting from Java 8 lambda expression added and created a much more concise
  alternative for most previous anonymous classes. It is known to be the biggest
  feature introduced with Java 8. It brings Functional Programming to Java.
date: '2021-09-23'
thumb_img_path: images/lambdas.png
thumb_img_alt: Java 8 lambdas
content_img_path: images/lambdas.png
content_img_alt: Java 8 lambdas
seo:
  title: Java 8 Lambdas
  description: >-
    Starting from Java 8 lambda expression added and created a much more concise
    alternative for most previous anonymous classes. It is known to be the
    biggest feature introduced with Java 8. It brings Functional Programming to
    Java.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: Java 8 lambdas
      keyName: property
    - name: 'og:description'
      value: >-
        Starting from Java 8 lambda expression added and created a much more
        concise alternative for most previous anonymous classes. It is known to
        be the biggest feature introduced with Java 8. It brings Functional
        Programming to Java.
      keyName: property
    - name: 'og:image'
      value: images/lambdas.png
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Java 8 lambdas
    - name: 'twitter:description'
      value: Java 8 lambdas
    - name: 'twitter:image'
      value: images/6.jpg
      relativeUrl: true
layout: post
---
Starting from Java 8 lambda expression added and created a much more concise alternative for most previous anonymous classes. It is known to be the biggest feature introduced with Java 8. It brings Functional Programming to Java.

# Lambdas Syntax

Here is a basic example of common code before Java 8:

```java
Predicate<String> isEmptyString =
    new Predicate<String>() {
      @Override
      public boolean apply(String str) {
        return str.isEmpty();
      }
    };
```

Java 8 comes to save us here and makes it a lot more elegant. We just need to use the -> to define the method like the following:

```java
Predicate<String> isEmptyString =
    (String str) -> {
      return str.isEmpty();
    };
```

## When can we use Lambdas?

We can use Lambdas because the following conditions are true:

*   `Predicate` is a "functional interface", meaning that it is an
    `interface` containing *exactly one* abstract method.
*   The lambda expression appears can easily infer the type based on
    `Predicate<String>`.

It is important to understand what is Functional Interfaces.

<div class="note">Any interface with one abstract method can be used with lambdas, but there is an annotation, `@FunctionalInterface`, to go on interfaces explicitly intended for this purpose. We recommend so annotating any interfaces in your project you explicitly intend to implement with lambdas.
</div>

## Can we make it more concise?

Lambdas can help us simplify a lot more. When the lambda expression contains exactly one statement, and the statement is returning a value or it is a void method call. Then we can remove the braces like the following:

```java
Predicate<String> p = (String str) -> str.isEmpty();
```

The Java compiler can infer the argument types so we can also remove that:

```java
Predicate<String> p = (str) -> str.isEmpty();
```

Finally since we only have a single parameter we can remove the parentheses like the following:

```java
Predicate<String> p = str -> str.isEmpty();
```

When we have a lambda that is just performing a direct method call, we can use a more compact syntax using a method reference. For example:

```java
Predicate<String> p = str -> str.isEmpty();
```

can be rewritten as the even simpler

```java
Predicate<String> p = String::isEmpty;
```

or we could rewrite

```java
BinaryOperator<BigInteger> add = (BigInteger a, BigInteger b) -> a.add(b);
```

more simply as

```java
BinaryOperator<BigInteger> add = BigInteger::add;
```

<div class="note">In general you want to remove code which increases cluter without adding to the readability. When possible we should use Lambdas to make the code more concise.</div>

## Show me more

Here is lambda with no parameters:

```java
Runnable runnable = () -> System.out.println("Hello");
```

As mentioned earlier we don't need the parentheses when there is a single parameter and the type can be inferred. Sometimes we cannot infer the type and we can cast:

```java
doSomething((Predicate<String>) str -> str.isEmpty());
```

## What are the limitations?

If a method has multiple overloads and accepts different lambda types. Then it would be difficult to automatically infer the type. We need to cast in these cases to make it work.

# Lambdas Best Practices

### Length and complexity

Lambdas expression are designed for small and simple bits of code. We cannot come up with a rule on the number of lines. But anytime you have some complexity you better off create a method and call that. We can always extract the complex lambda expression 

Lambda expressions are best used for small and simple bits of code. We don't
have a specific threshold in statements, lines, or any other measure. But your
own personal threshold (for when a lambda expression has become too complex)
should be considerably lower than your threshold for method bodies. A method can
"handle" a little more complexity, since it has a *name* and can have Javadoc
when needed. Lambdas don't have that.

Generally speaking, a too-complex lambda expression can be extracted into a
named method and replaced with a [reference](#method-references) to it. Lambdas
that reference local variables in the surrounding code (closures) cannot be
extracted as easily, but it is generally still worthwhile to explore
alternatives to large lambda bodies.

> Note: For what it's worth, [*Effective Java*](http://go/ej3e#page=217) has
> this to say:
>
> > If a computation isn’t self-explanatory, or exceeds a few lines, don’t put
> > it in a lambda. One line is ideal for a lambda, and three lines is a
> > reasonable maximum.