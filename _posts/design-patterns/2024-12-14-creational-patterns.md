---
layout: design_pattern
title: "creational patterns"
date: 2024-12-14
categories: design-patterns
---

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

### builder

- this pattern is for constructing complex objects step by step, where the instantion logic is a multi step operation as opposed to a single step used in factory methods.
- it prevents telescoping constructor anti-pattern cases such as:

```java
public function _construct(size, size,cheese = true, pepperoni = true, pepperoni=true,tomato = false, $lettuce = true)
{
}
```

imagine this all over the codebase, with random booleans and flags being passed in whenever a new `Burger` object is created. 👀 <br/>
we cant use subclasses with PnC here because the number of combinations will explode and extending this will not be scalable at all.

the logic is as follows:

- create a `Builder` interface, that has methods to set the properties of the `Building` object such as `setSize`, `buildDoors`, `buildWindows`, `buildRoofs` etc.
- create concrete builder classes that implement the `Builder` interface, such as `ConcreteBuilderA`, `ConcreteBuilderB`, `ConcreteBuilderC` etc.
- products are created by the builder classes, and the builder classes are responsible for the construction logic.

> **director** : this is the class that is responsible for creating the products with some predefined configs. the client can use the director to create the products, or the builder classes directly for further combinations of parameters.

- to use when there are several flavors of an object.
- to use when trying to avoid constructor telescoping.
- difference from the factory pattern is that; factory pattern is to be used when the creation is a one step process while builder pattern is to be used when the creation is a multi step process.

eg: complex usecases when building object trees with recursive construction step calling.

### prototype

- this pattern is for cloning objects without coupling to their concrete classes.

- logic is as follows:

  - create a prototype interface that has a `clone` method.
  - create concrete prototype classes that implement the prototype interface, with additional logic and properties based on the required use case.
  - the client is responsible for instantiating the prototype class and calling the `clone` method.

- to use when the cost of creating an object is expensive / labour intensive, and you want to avoid creating a new object from scratch.
- useful when you have 3rd party interfaces and the concrete classes are unknown.
- can use to reduce number of subclasses based on the type of configuration being used during initialization.

- **prototype registry** : this is a registry of prototype objects that are created at runtime, and can be cloned as required.
  - stores a list of all cloneable objects, and the client can request a clone of any of the objects in the list.
  - has a search method that searches for the object in the list based on some criteria, and returns the clone of the object.

eg: game development, where you want to clone a character and modify it into a different variant. I imagine this could be used in [procedural generation of levels](https://www.nomanssky.com/)

### singleton

- this pattern is for ensuring that a class has only one instance, and providing a global point of access to it.

- logic is as follows:

  - create a class with a private constructor, so that no other class can instantiate it.
  - create a static instance of the class in the same class.
  - create a static method that returns the instance of the class

- to use when you want to ensure that a class has only one instance - database connections, loggers, configs, etc. this pattern also providers better control over global variables.
- can also extend to "double-ton" pattern and so on, depending on the number of instances you want to create.
- eg: [nestjs modules are singletons by default](https://docs.nestjs.com/modules#shared-modules) - very big part of the framework is built around this pattern.
