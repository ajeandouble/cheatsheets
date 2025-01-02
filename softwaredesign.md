# Clean Code

# Software design

## Clean Code

### Code hygiene

- Meaningful naming
	- Descriptive names for entities: convey purpose and functionality
- Functions and methods
	- Shorts and focused on a single task
	- Avoid deep nesting
	- Functions should do one thing only and do it well
		- Avoid long, monolithic functions
- Comments
	- Strive to make the code self-explanatory
	- Only document non-obvious parts
- Follow formatting guidelines
- Delete *dead code*
- ***DRY***: Don't Repeat Yourself
	- Avoid code duplication
- Write tests
- Refactor the code
	- Continuous refactoring without changing the code extern behaviour

## SOLID principles

- **S**.	Separation of Concern

	> A Class should have one responsibility (one task)
	- It avoids writing a slightly different Class when a task changes

- **O**.	Open/Closed principle

	> Classes should be open for extension, not modification
	- We should factor our Classes hierarchy to specialize subclasses instead of using conditions

- **L**. Liskov Substition Principle

	> Subtypes should be substitutable from their base Types
	- We can re-use base type methods and properties with a subtype object
	- It ensures well-functionning of polymorphism

- **I**.	Interface Segregation Principle

	> Clients should not be forced to depend upon methods that they do not use
	-  Do not force subtypes to implement methods and properties that they might not need

- **D**. Dependency Injection Principle

	> Abstractions should not depend upon details. Details should depend upon abstractions
	- A Class shouldn't depend upon another class implementation details but should

## Testing

## Best Practices

- Isolation

	> Tests should be isolated, not relying on external data or state.
	
- Fast and Repeatable
	
	>Tests should run quickly and produce the same results every time.
	
- Readable and Maintainable

	> Write tests that are easy to understand and modify.

- Clear Naming
	> Use descriptive names for test methods.

- Single Responsibility
	> Test one thing at a time.

- Coverage
	> Aim for high test coverage to catch more bugs.

- Unit Testing: Testing individual units or components of code in isolation to ensure their correctness.
- Integration Testing: Testing the interaction between multiple components to ensure they work together as expected.
- Functional Testing: Testing the software's functionality against the requirements.
- Regression Testing: Ensuring that new code changes do not break existing functionality.


# Software Design

## Complexity

>Complexity comes from an accumulation of ***dependencies and obscurities***. As complexity increases, it leads to change amplification, a high cognitive load, and unknown unknowns. As a result, it takes more code modifications to implement each new feature. In addition, developers spend more time acquiring enough information to make the change safely and, in the worst case, they can’t even find all the information they need. The bottom line is that complexity makes it difficult and risky to modify an existing code base.

### Symptoms of complexity

**Change amplification:**  a seemingly simple change requires code modifications in many different place.
**Cognitive load:**  how much a developer needs to know in order to complete a task.

> System designers sometimes assume that complexity can be measured by lines of code. (...) I have seen frameworks that allowed applications to be written with only a few lines of code, but it was extremely difficult to figure out what those lines were. Sometimes an approach that requires more lines of code is actually simpler, because it reduces cognitive load.

## Strategic vs tactical design

>Many organizations encourage a tactical mindset, focused on getting features working as quickly as possible. However, if you want a good design, you must take a more strategic approach where you invest time to produce clean designs and fix problems.

### Tactical programming (short-sightedness)

>You don’t spend much time looking for the best design; you just want to get something working soon.
>Each of them probably seems like a reasonable compromise in order to finish the current task quickly. However, the complexities accumulate rapidly, especially if everyone is programming tactically.

### Strategic programming (working code isn't enough)

>The most important thing is the long-term structure of the system. Most of the code in any system is written by extending the existing code base, so your most important job as a
developer is to facilitate those future extensions.
>***Investment mindset*** (...) Rather than taking the fastest path to finish your current project, you must invest time to improve the design of the system. 

### How to invest?

>A huge up-front investment, such as trying to design the entire system, won’t be effective.
>I suggest spending about 10–20% of your total development time on investments. This amount is small enough that it won’t impact your schedules significantly, but large enough to produce significant benefits over time.

### Startup tactical mindset

>For example, early-stage startups feel tremendous pressure to get their early releases out quickly. In these companies, it might seem that even a 10–20% investment isn’t affordable. As a result, many startups take a tactical approach, spending little effort on design and even less on cleanup when problems pop up. They rationalize this with the thought that, if they are successful, they’ll have enough money to hire extra engineers to clean things up.
>One of the most important factors for success of a company is the quality of its engineers. The best way to lower development costs is to hire great engineers: they don’t cost much more than mediocre engineers but have tremendously higher productivity. However, the ***best engineers care deeply about good design***. If your code base is a wreck, word will get out, and this will make it harder for you to recruit.


## Modular design

>The goal of modular design is to minimize the dependencies between modules.
>In order to manage dependencies, we think of each module in two parts: an interface and an implementation.

### Abstraction

>An abstraction is a simplified view of an entity, which omits unimportant details. 

### Deep vs Shallow modules

>The best modules are deep: they allow a lot of functionality to be accessed through a simple interface. A shallow module is one with a relatively complex interface, but not much functionality: it doesn’t hide much complexity.
>Module depth is a way of thinking about cost versus benefit. The benefit provided by a module is its functionality. The cost of a module (in terms of system complexity) is its interface.

#### Red Flag: Shallow Module

>A shallow module is one whose interface is complicated relative to the functionality it provides. Shallow modules don’t help much in the battle against complexity, because the benefit they provide (not having to learn about how they work internally) is negated by the cost of learning and using their interfaces. Small modules tend to be shallow.

#### "Classitis"

>Students are often taught that the most important thing in class design is to break up larger classes into smaller ones. The same advice is often given about methods: “Any method longer than N lines should be divided into multiple methods” (N can be as low as 10). This approach results in large numbers of shallow classes and methods, which add to overall system complexity.


## Information hiding

>Each module should encapsulate a few pieces of knowledge, which represent design decisions. The knowledge is embedded in the module’s implementation but does not appear in its interface, so it is not visible to other modules.

### Private vs public

>Hiding variables and methods in a class by declaring them private isn’t the same thing as information hiding. Private elements can help with information hiding, since they make it impossible for the items to be accessed directly from outside the class. However, information about the private items can still be exposed through public methods such as getter and setter methods.
>The best form of information hiding is when information is totally hidden within a module, so that it is irrelevant and invisible to users of the module.

### Red flag: Information leakage
>Information leakage occurs when the same knowledge is used in multiple places, such as two different classes that both understand the format of a particular type of file.


### Redflag: Temporal decomposition

>In temporal decomposition, execution order is reflected in the code structure: operations that happen at different times are in different methods or classes. If the same knowledge is used at different points in execution, it gets encoded in multiple places, resulting in information leakage.

>We propose instead that one begins with a list of difficult design decisions or design decisions which are likely to change. Each module is then designed to hide such a decision from the others. Since, in most cases, design decisions transcend time of execution, modules will not correspond to steps in the processing. To achieve an efficient implementation we must abandon the assumption that a module is one or more subroutines, and instead allow subroutines and programs to be assembled collections of code from various modules

[Criteria for modularization - D.L. Parnas](https://wstomv.win.tue.nl/edu/2ip30/references/criteria_for_modularization.pdf)

### Red flag: Overexposure

>If the API for a commonly used feature forces users to learn about other features that are rarely used, this increases the cognitive load on users who don’t need the rarely used features.

### Conclusion

>When decomposing a system into modules, try not to be influenced by the order in which operations will occur at runtime; that will lead you down the path of temporal decomposition, which will result in information leakage and shallow modules. Instead, think about the different pieces of knowledge that are needed to carry out the tasks of your application, and design each module to encapsulate one or a few of those pieces of knowledge.

See: [On the Criteria to be Used in Decomposing Systems into Modules - David Parnas](https://wstomv.win.tue.nl/edu/2ip30/references/criteria_for_modularization.pdf)

## General-Purpose modules are deeper

>One of the most common decisions that you will face when designing a new module is whether to implement it in a general-purpose or special-purpose fashion. 

### General purpose modules

>The sweet spot is to implement new modules in a somewhat general-purpose fashion.

### Questions to ask yourself

- *What is the simplest interface that will cover all my current needs?*
- *In how many situations will this method be used?*
- *Is this API easy to use for my current needs?*

### Red flag: Pass-through method and variables

>A pass-through method is one that does nothing except pass its arguments to another method, usually with the same API as the pass-through method. This typically indicates that there is not a clean division of responsibility between the classes.
>Pass-through variables add complexity because they force all of the intermediate methods to be aware of their existence, even though the methods have no use for the variables

### Decorators

>Decorator classes often contain many pass-through methods. It’s easy to overuse the decorator pattern, creating a new class for every small new feature.

### Conclusion

>The “different layer, different abstraction” rule is just an application of this idea: if different layers have the same abstraction, such as pass-through methods or decorators, then there’s a good chance that they haven’t provided enough benefit to compensate for the additional infrastructure they represent. 

## Pull Complexity Downwards

>It is more important for a module to have a simple interface than a simple implementation.
>When developing a module, ***look for opportunities to take a little bit of extra suffering upon yourself in order to reduce the suffering of your users.***


## Modules splitting

>The decision to split or join modules should be based on complexity. Pick the structure that results in the best information hiding, the fewest dependencies, and the deepest interfaces.
>Each method should do one thing and do it completely. The method should have a clean and simple interface, so that users don’t need to have much information in their heads in order to use it correctly.

See separation of concern.

>Splitting up a method only makes sense if it results in cleaner abstractions, overall. 

### DRY


>If the same piece of code (or code that is almost the same) appears over and over again, that’s a red flag that you haven’t found the right abstractions.

### Red flag: Special-General mixsture

>This red flag occurs when a general-purpose mechanism also contains code specialized for a particular use of that mechanism. This makes the mechanism more complicated and creates information leakage between the mechanism and the particular use case: future modifications to the use case are likely to require changes to the underlying mechanism as well.

### Red flag: Conjoined Methods

It should be possible to understand each method independently. If you can’t understand the implementation of one method without also understanding the implementation of another, that’s a red flag. This red flag can occur in other contexts as well: if two pieces of code are physically separated, but each can only be understood by looking at the other, that is a red flag.


## Exceptions

>**Throwing exceptions is easy; handling them is hard.**

>The exceptions thrown by a class are part of its interface; classes with lots of exceptions have complex interfaces, and they are shallower than classes with fewer exceptions.

>**Overall, the best way to reduce bugs is to make software simpler.**



# The myth of the man month

