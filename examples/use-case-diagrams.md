---
title: UML Use Case Diagrams
subtitle: using PlantUML
author: Ingo Kofler
---

# Models

## What is a model?

* a concrete or abstract copy of an existing entity
* a concrete or abstract ideal of an entity to be created

## Which properties does a model have?

1. every model needs to have a corresponding original
1. the model does not include every detail of the original (_abstraction_)
1. every model serves a concrete purpose (_pragmatism_)

## Discussion

Discuss the three properties in the context of

* a hiking map
* a remote-controlled car

# Use Case Diagrams

## Unified Modeling Language

* defines 14 diagram types covering both structure and behaviour aspects
* de-facto standard in Software Engineering
* established in late 1990s
* actively developed by the Object Management Group (OMG)

## Scope

* graphical modeling of the system's functionality
* comprehensible also for non-technical experts
* mostly used in requirements engineering

* main focus on
  * who are the actors?
  * what are functional blocks?
  * any connections to external systems?

## Example

```{ .plantuml height=500 plantuml-filename=uc-simple.png }
actor "Account Manager" as accountmgr
actor "Customer" as customer

rectangle "Simple Banking System" {
    usecase lending
    usecase "credit information" as creditinfo
}

creditinfo -[hidden]up- lending

lending -right- customer
lending -left- accountmgr
creditinfo -left- accountmgr

```

## Elements

* actors
  * represent a role of users
  * can be humans or external systems
* use cases
  * achieves a (business) goal of an actor
  * involvement of one or multiple actors
  * can include or extend each other
* system boundary
  * explicitly states what's in or not

## Advanced Example

```{ .plantuml height=500 plantuml-filename=uc-advanced.png }
actor "Account Manager" as accountmgr
actor "Customer" as customer
actor "Bank Manager " as bankmgr
actor "Employee" as emp

rectangle "Advanced Banking System" {
    usecase lending
    usecase "risk credit approval" as rca
    usecase "credit screening" as cs
}

emp <|- accountmgr
emp <|- bankmgr

lending -right- customer
lending -left- accountmgr
lending <.down. rca : extends
lending .up.> cs  : includes
rca -left- bankmgr
```

# PlantUML

## What is it?

* software tool to create simple UML diagrams
* no visual editing but specification by code
* automatic rendering and layouting

## Code Example

```
actor "Account Manager" as accountmgr
actor "Customer" as customer
actor "Bank Manager" as bankmgr

rectangle "Advanced Banking System" {
    usecase lending
    usecase "risk credit approval" as rca
    usecase "credit screening" as cs
}

lending -right- customer
lending -left- accountmgr
lending <.down. rca : extends
lending .up.> cs  : includes
rca -left- bankmgr
```

## Results in

```{ .plantuml height=500 plantuml-filename=uc-example.png }
actor "Account Manager" as accountmgr
actor "Customer" as customer
actor "Bank Manager" as bankmgr

rectangle "Advanced Banking System" {
    usecase lending
    usecase "risk credit approval" as rca
    usecase "credit screening" as cs
}

lending -right- customer
lending -left- accountmgr
lending <.down. rca : extends
lending .up.> cs  : includes
rca -left- bankmgr

```

## How to develop

* Online Tools
  * <http://www.plantuml.com>
  * <http://www.planttext.com>
* Extensions / Plugins
  * IntelliJ
  * Visual Studio Code
  * and many more...
