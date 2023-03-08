# Lesson 25

So far, we have looked at analyzing problems, modeling in UML, and designing architectural solutions. Now we want to look at the actual process of designing objects. To get started, we will do an exercise from Robert Martin that involves designing software to control a coffee maker.

## Two Approaches

We can begin with OOA (finding the nouns in the product description). The alternative approach is the **role-based design** approach which advocates using uses cases to build up our diagram rather than starting with the nouns.

## Class Model Diagram

The class model diagram for the coffee maker includes the following classes: `Button`, `Light`, `CoffeeMaker`, `Boiler`, `WarmerPlate`, `BoilerSensor`, `BoilerHeater`, `PlateHeater`, `PlateSensor`, `Heater`, and `Sensor`.

## Role-based Design

Role-based design can be performed through the following steps:

1. Lay out use cases
2. For each use case, construct a collaboration diagram
3. Think of the collaboration diagram instead as a class model diagram
4. Each class can then be thought of as participating in a variety of roles
5. The overall class behavior is the sum of its roles

## Dependency Inversion Principle

For the coffee maker problem it is better to design classes based on a set of behaviors. The design is of value by itself so we should subclass it for each specific coffee maker. High-level modules should not depend on low-level ones. Note that this is the opposite philosophy from layered architectures, where high-level modules are built on top of low-level ones.

## Realization

How do we go about figuring out if we should be using the dependency inversion principle?

1. We express what we have done so far as abstract classes
2. We subclass each of them for our product
3. The subclass versions implement the abstract methods by calling the API
4. Subclasses use calls to the abstract methods

## Refinement

Here is what Martin has to say about the dependency inversion principle regarding the coffee maker problem:

> None of the three classes we have created must ever know anything about the Mark VI. This is the DIP (Dependency Inversion Principle). We are not going to allow the high-level coffee making policy of this system to depend upon the low-level implementation.

## Summary

Using traditional OOA does not always lead to the best solution. Think about using use cases to determine roles. You might have to use DIP to reduce coupling and promote reuse.

## Section Quizzes

The Mark IV Special Coffee Maker (Textual Description):

> The Mark IV Special Coffee Maker makes up to 12 cups of coffee at a time. The user places a filter in the filter holder, fills the filter with coffee grounds, and slides the filter holder into its receptacle. The user then pours up to 12 cups of water into the water strainer and presses the Brew button. The water is heated until boiling. The pressure of the evolving steam forces the water to be sprayed over the coffee grounds, and coffee drips through the filter into the pot. The pot is kept warm for extended periods by a warmer plate, which only turns on if there is coffee in the pot. If the pot is removed from the warmer plate while water is being sprayed over the grounds, the flow of water is stopped so that brewed coffee does not spill on the warmer plate.

### Hardware Quiz

_One way of attacking a problem like this is from the bottom up. That is, you are given a device for which you are going to provide software support, so you determine what its capabilities are. Make a list of all the hardware devices that are part of the coffee maker_.

Coffee maker, filter, filter holder, receptacle, water strainer, brew button, pot, and warmer plate.

### Traditional Approach Quiz

_The traditional OOA approach to modeling is to search for nouns (or noun phrases) in the problem statement and model them with classes. Do this now on the coffee maker description producing a list of nouns or noun phrases_.

`CoffeeMaker`, `Cups`, `Coffee`, `Filter`, `FilterHolder`, `Receptacle`, `WaterStrainer`, `BrewButton`, `Pot`, and `WarmerPlate`.

### Limitations Quiz

_One of the points of Martin's exercises is the limitations of the traditional approach. See how many problems you can detect with this design (shown in lecture)_.

There does not seem to be any attributes or methods in this diagram. Furthermore, it seems like the key objects such as coffee or coffee grounds, water, filter, cups, and pot is missing from the diagram.

### Brew Button Quiz

_Let's look at the first use case: user presses the brew button, and play through what happens. First off, which of the three classes receives this event from the hardware interface_?

User interface should be responsible for delegating tasks.

### Hardware API Quiz

_To proceed with our object design, we could implement the described behaviors (of the coffee maker) as methods in each of the three classes by having them make calls to the hardware API. This would be the wrong approach. Why_?

The coupling would be too tight between the client code and the specific hardware.
