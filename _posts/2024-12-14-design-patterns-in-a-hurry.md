---
layout: post
title: "design patterns in a hurry"
date: 2024-12-14
categories: tech
---

humans -> pattern recognition during problem solving -> repeatability over time -> ✨ design patterns ✨. first came about in architecture, where a language was made using patterns as its units. it was later picked up by software engineers.

kind of a double edged sword, because if used correctly, it makes things a lot easier, if not, it's creates technical debt.

> If all you have is a hammer, everything looks like a nail.

in my experience, some design patterns are frequently used within the same codebase, while others are rarely utilized. this is likely because the authors of the codebase have a preferred way of doing things, which they continue to follow as the company grows.

it is beneficial to be aware of such patterns, as they help create a good structure for information flow. startups focus on speed, whereas larger companies focus on code maintainability and scalability - utilise patterns accordingly, as everything is a tradeoff.

this post is a a quick refresher on design patterns, I learned from [this repo](https://github.com/kamranahmedse/design-patterns-for-humans) and [this website](https://refactoring.guru/design-patterns/what-is-pattern).

### types of design patterns

- [creational](#creational) : related to object(s) instantiation
- [structural](#structural) : related to object(s) composition, how entities can use each other. think "components".
- [behavioral](#behavioral) : related to object(s) responsibilities, how they can interact with each other.

### creational

some basic terminology:

- **product** : the object being created, can have different variants.
- **factory** : function, method or class that supposed to be producing something. factories produce objects with some common logic.
- **creation method / factory method** : a method that creates an object. the creation method is just a wrapper around a constructor call, put in place for logical isolation.
- **simple factory** : basically a class that implements an interface with a static creation method.

#### factory method

- this pattern is for instantiating factories that create different products with some common logic, based on runtime conditions

- logic is as follows:

  - create a product interface (A) (that implements the common logic of the products) - all products need to implement this.
  - create a factory interface (B), that has a `createProduct` "factory method" with return type of product interface A
  - create factory classes from (B) - these will be instantiated at runtime as required and return the right product instances.

- the client is concerned with the interface (A) and does not care about the concrete factory classes being created. that gets decided at runtime via the factory subclass.
- follows single responsibility principle (the factory is responsible for creating products, not the client), and open/closed principle (open for extension, closed for modification)
- eg: cross platform UI components (different buttons for mac, windows, linux)

#### abstract factory

- this pattern lets you produce families of related objects without specifying their concrete classes. its a factory of factories where the products families are grouped together due to some underlying relationship.

- logic is as follows:

  - create product interfaces for each product family (A1, A2, A3 ... ) where all product variants need to implement these.
  - create abstract factory interface (B) - this has creation methods for all the product families; `createProductA1()`, `createProductA2()`...
  - for each variant of the product family, create factory classes that implement the abstract factory interface (B) where the returned products are from the related family variants.
    - signatures of their creation methods must return corresponding abstract products, so that the client is not coupled to the specific variants of the product families.

- the client is exposed to the abstract interfaces, and the application is responsible for instantiating the correct factory class at initialization, based on runtime settings / environment variables.
- usually when implementing a lot of factories, the abstract factory pattern is used to group them into families so that the client can just use the abstract factory interface and not worry about the grouping logic.
- follows single responsibility principle (the abstract factory is responsible for creating products and families, not the client), and open/closed principle (open for extension, closed for modification)
- eg: cross platform UI libraries with extensible components, where the concrete UI components are grouped into families based on their platform (mac, windows, linux)

#### builder

- this pattern is for constructing complex objects step by step, where the instantion logic is a multi step operation as opposed to a single step used in factory methods.
- it prevents telescoping constructor anti-pattern cases such as:

```java
public function \_\_construct(size, size,cheese = true, pepperoni = true, pepperoni=true,tomato = false, $lettuce = true)
{
}
```

imagine this all over the codebase, with random booleans and flags being passed in whenever a new `Burger` object is created. 👀 <br/>
we cant use subclasses with PnC here because the number of combinations will explode and extending this will not be scalable at all.

the logic is as follows:

- create a `Builder` interface, that has methods to set the properties of the `Building` object such as `setSize`, `buildDoors`, `buildWindows`, `buildRoofs` etc.
- create concrete builder classes that implement the `Builder` interface, such as `ConcreteBuilderA`, `ConcreteBuilderB`, `ConcreteBuilderC` etc.
- products are created by the builder classes, and the builder classes are responsible for the construction logic.
- **director** : this is the class that is responsible for creating the products with some predefined configs.
- the client can use the director to create the products, or the builder classes directly for further combinations of parameters.

- to use when there are several flavors of an object.
- to use when trying to avoid constructor telescoping.
- difference from the factory pattern is that; factory pattern is to be used when the creation is a one step process while builder pattern is to be used when the creation is a multi step process.

eg: complex usecases when building object trees with recursive construction step calling.

### structural

### behavioral
