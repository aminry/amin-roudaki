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

