---
title: Java 8 Lambdas
excerpt: >-
  Hiking can sometimes involves bushwhacking and hiking is sometimes referred to
  as such. This specifically refers to difficult walking through dense forest,
  undergrowth, or bushes, where forward progress requires pushing vegetation
  aside.
date: '2018-01-09'
thumb_img_path: images/6.jpg
thumb_img_alt: Hikers on the trail
content_img_path: images/6.jpg
content_img_alt: Hikers on the trail
seo:
  title: Basic Rules For Walking In The Mountains
  description: >-
    Hiking refers to difficult walking through dense forest, undergrowth, or
    bushes.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: Basic Rules For Walking In The Mountains
      keyName: property
    - name: 'og:description'
      value: >-
        Hiking refers to difficult walking through dense forest, undergrowth, or
        bushes.
      keyName: property
    - name: 'og:image'
      value: images/6.jpg
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Basic Rules For Walking In The Mountains
    - name: 'twitter:description'
      value: >-
        Hiking refers to difficult walking through dense forest, undergrowth, or
        bushes.
    - name: 'twitter:image'
      value: images/6.jpg
      relativeUrl: true
layout: post
---

Photo by [David Marcu.](https://unsplash.com/photos/wcHCzgo0_mQ)

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

## Why can we use Lambdas?
We can use Lambdas because the following conditions are true:
*   `Predicate` is a "functional interface", meaning that it is an
    `interface` containing *exactly one* abstract method.
*   The lambda expression appears can easily infer the type based on 
    `Predicate<String>`.

It is important to understand what is a Functional Interfaces.

<div class="note">Any interface with one abstract method can be used with lambdas, but there is an annotation, `@FunctionalInterface`, to go on interfaces explicitly intended for this purpose. We recommend so annotating any interfaces in your project you explicitly intend to implement with lambdas.
</div>

# Can we make it more concise?

Lambdas can help us simplify a lot more. When the lambda expression contains exactly one statement, and the statement is returning a value or it is a void method call. Then we can remove the braces like the following:

```java
Predicate<String> p = (String str) -> str.isEmpty();
```

The Java compiler can infer the argument types if it can:

```java
Predicate<String> p = (str) -> str.isEmpty();
```

Lastly, when there is exactly one parameter, with an inferred type, then even
the parentheses around the parameter list can go:

```java
Predicate<String> p = str -> str.isEmpty();
```

We will see on the [next page](method-refs.md) that this particular example can
be simplified even further!

When you *can* omit some code, does that mean you should? Remember, conciseness
is the reason lambda expressions were added to Java. So in general, you should
omit clutter when you can. But follow the same guideline as we use for
non-required grouping parentheses: if you *or* your reviewer feels that the
extra code improves readability, go ahead and include it.

## More examples {#more}

This lambda takes no parameters:

```java
Runnable runnable = () -> System.out.println("Hello");
```

Recall that parentheses are optional only when there is exactly one parameter,
of inferred type. And we can omit the braces, because the body is a single
method call.

Target typing may sometimes fail, but you can point the way using a cast:

```java
doSomething((Predicate<String>) str -> str.isEmpty());
```

When will it fail? The most common case is when there are multiple overloads
accepting different lambda types (a scenario you should try to avoid when
overloading lambda-accepting methods). But in general, Java 8's new smarter type
inference is sort of a black box: it's smart but in difficult-to-predict ways.
We really don't have any better advice than "try it without explicit types, then
add explicit types back in until it works."

## Differences vs. anonymous classes {#vs_class}

As mentioned above, you can *mostly* think of a lambda expression or method
reference as a concise anonymous class. But there are a few differences:

*   Lambda expressions are treated as identityless. References to `this` (both
    explicitly and implicitly) inside a lambda expression refer to the
    *containing* instance, not the lambda instance.

*   Instances of both anonymous classes and lambda expressions "capture" state
    from the surrounding context when they are created -- copying and retaining
    references to variables[^2] so they can be used later. But lambda
    expressions are much smarter about capturing only the state they will really
    need, which often may be no state at all. This should plug more than a few
    memory leaks!

*   If a lambda *can* be extracted to a static constant and reused, the VM will
    usually make that optimization automatically. You should still make a
    constant for a lambda expression when you feel that it helps *readability*,
    but there is no need to do so purely for performance reasons.

*   In theory, lambda expressions can incur greater startup cost (a class is
    generated on the fly). This has not seemed to be a significant problem for
    any projects we're aware of.

*   Lambda expressions yield fairly useless debugging output (`toString` and
    stack traces) such as `Foo$$Lambda$5/1044036744`. Unlike with classes, there
    are really no options for improving this. Of course, what's most important
    in a stack trace are the exception messages, filenames, and line numbers,
    and those are all intact.

*   You'll still need to use classes in plenty of situations: when you have more
    than one method to implement, when you are implementing an abstract class,
    when you need state, etc.

[^2]: In Java 7, you had to mark local variables as `final` for them to be
    eligible for capture by an anonymous class. In Java 8, the compiler will
    automatically infer when local variables can be `final`, so this is no
    longer necessary for lambdas _or_ anonymous classes. In this case, the
    variable is called
    [effectively final](other-language.md#effectively-final-variables).

## External tutorial

A more detailed tutorial on the use of lambda expressions can be found
[here](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/Lambda-QuickStart/index.html).
<!-- TODO(kevinb): find and agree on the best resource we can -->

--------------------------------------------------------------------------------

Please continue to the next page, [Method references](method-refs.md), or choose
another topic in the sidebar.

--------------------------------------------------------------------------------
