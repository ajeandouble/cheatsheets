# Notions

## Orthogonality

- Features can be used independently
- Combining features has predictable results
- Changing one thing doesn't unexpectedly affect another
- Components have clear, non-overlapping responsibilities


# A Philosophy of Software Design - John Ousterhout

> The reward for being a good designer is that you get to spend a larger fraction of your time in the design phase, which is fun. Poor designers spend most of their time chasing bugs in complicated and brittle code. If you improve your design skills, not only will you produce higher quality software more quickly, but the software development process will be more enjoyable.

## Complexity

> Complexity comes from an accumulation of **_dependencies and obscurities_**. As complexity increases, it leads to change amplification, a high cognitive load, and unknown unknowns. As a result, it takes more code modifications to implement each new feature. In addition, developers spend more time acquiring enough information to make the change safely and, in the worst case, they can’t even find all the information they need. The bottom line is that complexity makes it difficult and risky to modify an existing code base.

### Symptoms of complexity

**Change amplification:** a seemingly simple change requires code modifications in many different place.
**Cognitive load:** how much a developer needs to know in order to complete a task.

> System designers sometimes assume that complexity can be measured by lines of code. (...) I have seen frameworks that allowed applications to be written with only a few lines of code, but it was extremely difficult to figure out what those lines were. Sometimes an approach that requires more lines of code is actually simpler, because it reduces cognitive load.

## Strategic vs tactical design

> Many organizations encourage a tactical mindset, focused on getting features working as quickly as possible. However, if you want a good design, you must take a more strategic approach where you invest time to produce clean designs and fix problems.

### Tactical programming (short-sightedness)

> You don’t spend much time looking for the best design; you just want to get something working soon.
> Each of them probably seems like a reasonable compromise in order to finish the current task quickly. However, the complexities accumulate rapidly, especially if everyone is programming tactically.

### Strategic programming (working code isn't enough)

> The most important thing is the long-term structure of the system. Most of the code in any system is written by extending the existing code base, so your most important job as a
> developer is to facilitate those future extensions.
> **_Investment mindset_** (...) Rather than taking the fastest path to finish your current project, you must invest time to improve the design of the system.

### How to invest?

> A huge up-front investment, such as trying to design the entire system, won’t be effective.
> I suggest spending about 10–20% of your total development time on investments. This amount is small enough that it won’t impact your schedules significantly, but large enough to produce significant benefits over time.

### Startup tactical mindset

> For example, early-stage startups feel tremendous pressure to get their early releases out quickly. In these companies, it might seem that even a 10–20% investment isn’t affordable. As a result, many startups take a tactical approach, spending little effort on design and even less on cleanup when problems pop up. They rationalize this with the thought that, if they are successful, they’ll have enough money to hire extra engineers to clean things up.
> One of the most important factors for success of a company is the quality of its engineers. The best way to lower development costs is to hire great engineers: they don’t cost much more than mediocre engineers but have tremendously higher productivity. However, the **_best engineers care deeply about good design_**. If your code base is a wreck, word will get out, and this will make it harder for you to recruit.

## Modular design

> The goal of modular design is to minimize the dependencies between modules.
> In order to manage dependencies, we think of each module in two parts: an interface and an implementation.

### Abstraction

> An abstraction is a simplified view of an entity, which omits unimportant details.

### Deep vs Shallow modules

> The best modules are deep: they allow a lot of functionality to be accessed through a simple interface. A shallow module is one with a relatively complex interface, but not much functionality: it doesn’t hide much complexity.
> Module depth is a way of thinking about cost versus benefit. The benefit provided by a module is its functionality. The cost of a module (in terms of system complexity) is its interface.

#### Red Flag: Shallow Module

> A shallow module is one whose interface is complicated relative to the functionality it provides. Shallow modules don’t help much in the battle against complexity, because the benefit they provide (not having to learn about how they work internally) is negated by the cost of learning and using their interfaces. Small modules tend to be shallow.

#### "Classitis"

> Students are often taught that the most important thing in class design is to break up larger classes into smaller ones. The same advice is often given about methods: “Any method longer than N lines should be divided into multiple methods” (N can be as low as 10). This approach results in large numbers of shallow classes and methods, which add to overall system complexity.

## Information hiding

> Each module should encapsulate a few pieces of knowledge, which represent design decisions. The knowledge is embedded in the module’s implementation but does not appear in its interface, so it is not visible to other modules.

### Private vs public

> Hiding variables and methods in a class by declaring them private isn’t the same thing as information hiding. Private elements can help with information hiding, since they make it impossible for the items to be accessed directly from outside the class. However, information about the private items can still be exposed through public methods such as getter and setter methods.
> The best form of information hiding is when information is totally hidden within a module, so that it is irrelevant and invisible to users of the module.

### Red flag: Information leakage

> Information leakage occurs when the same knowledge is used in multiple places, such as two different classes that both understand the format of a particular type of file.

### Redflag: Temporal decomposition

> In temporal decomposition, execution order is reflected in the code structure: operations that happen at different times are in different methods or classes. If the same knowledge is used at different points in execution, it gets encoded in multiple places, resulting in information leakage.

> We propose instead that one begins with a list of difficult design decisions or design decisions which are likely to change. Each module is then designed to hide such a decision from the others. Since, in most cases, design decisions transcend time of execution, modules will not correspond to steps in the processing. To achieve an efficient implementation we must abandon the assumption that a module is one or more subroutines, and instead allow subroutines and programs to be assembled collections of code from various modules

[Criteria for modularization - D.L. Parnas](https://wstomv.win.tue.nl/edu/2ip30/references/criteria_for_modularization.pdf)

### Red flag: Overexposure

> If the API for a commonly used feature forces users to learn about other features that are rarely used, this increases the cognitive load on users who don’t need the rarely used features.

### Conclusion

> When decomposing a system into modules, try not to be influenced by the order in which operations will occur at runtime; that will lead you down the path of temporal decomposition, which will result in information leakage and shallow modules. Instead, think about the different pieces of knowledge that are needed to carry out the tasks of your application, and design each module to encapsulate one or a few of those pieces of knowledge.

See: [On the Criteria to be Used in Decomposing Systems into Modules - David Parnas](https://wstomv.win.tue.nl/edu/2ip30/references/criteria_for_modularization.pdf)

## General-Purpose modules are deeper

> One of the most common decisions that you will face when designing a new module is whether to implement it in a general-purpose or special-purpose fashion.

### General purpose modules

> The sweet spot is to implement new modules in a somewhat general-purpose fashion.

### Questions to ask yourself

- _What is the simplest interface that will cover all my current needs?_
- _In how many situations will this method be used?_
- _Is this API easy to use for my current needs?_

### Red flag: Pass-through method and variables

> A pass-through method is one that does nothing except pass its arguments to another method, usually with the same API as the pass-through method. This typically indicates that there is not a clean division of responsibility between the classes.
> Pass-through variables add complexity because they force all of the intermediate methods to be aware of their existence, even though the methods have no use for the variables

### Decorators

> Decorator classes often contain many pass-through methods. It’s easy to overuse the decorator pattern, creating a new class for every small new feature.

### Conclusion

> The “different layer, different abstraction” rule is just an application of this idea: if different layers have the same abstraction, such as pass-through methods or decorators, then there’s a good chance that they haven’t provided enough benefit to compensate for the additional infrastructure they represent.

## Pull Complexity Downwards

> It is more important for a module to have a simple interface than a simple implementation.
> When developing a module, **_look for opportunities to take a little bit of extra suffering upon yourself in order to reduce the suffering of your users._**

## Modules splitting

> The decision to split or join modules should be based on complexity. Pick the structure that results in the best information hiding, the fewest dependencies, and the deepest interfaces.
> Each method should do one thing and do it completely. The method should have a clean and simple interface, so that users don’t need to have much information in their heads in order to use it correctly.

See separation of concern.

> Splitting up a method only makes sense if it results in cleaner abstractions, overall.

### DRY

> If the same piece of code (or code that is almost the same) appears over and over again, that’s a red flag that you haven’t found the right abstractions.

### Red flag: Special-General mixsture

> This red flag occurs when a general-purpose mechanism also contains code specialized for a particular use of that mechanism. This makes the mechanism more complicated and creates information leakage between the mechanism and the particular use case: future modifications to the use case are likely to require changes to the underlying mechanism as well.

### Red flag: Conjoined Methods

It should be possible to understand each method independently. If you can’t understand the implementation of one method without also understanding the implementation of another, that’s a red flag. This red flag can occur in other contexts as well: if two pieces of code are physically separated, but each can only be understood by looking at the other, that is a red flag.

## Exceptions

> **Throwing exceptions is easy; handling them is hard.**

> The exceptions thrown by a class are part of its interface; classes with lots of exceptions have complex interfaces, and they are shallower than classes with fewer exceptions.

> **Overall, the best way to reduce bugs is to make software simpler.**

> The best way to do this is by redefining semantics to eliminate error conditions. For exceptions that can’t be defined away, you should look for opportunities to mask them at a low level, so their impact is limited, or aggregate several special-case handlers into a single more generic handler. Together, these techniques can have a significant impact on overall system complexity.

## Design it Twice

> After you have roughed out the designs for the alternatives, make a list of the pros and cons of each one. The most important consideration for an interface is ease of use for higher level software.

> The design-it-twice approach not only improves your designs, but it also improves your design skills. The process of devising and comparing multiple approaches will teach you about the factors that make designs better or worse. Over time, this will make it easier for you to rule out bad designs and hone in on really great ones.

## Comments

> Good comment is self-documenting

> The overall idea behind comments is to capture information that was in the mind of the designer but couldn’t be represented in the code.

> Developers should be able to understand the abstraction provided by a module without reading any code other than its externally visible declarations. **_The only way to do this is by supplementing the declarations with comments._**

### Red Flag: Comment repeats code

> If the information in a comment is already obvious from the code next to the comment, then the comment isn’t helpful. One example of this is when the comment uses the same words that make up the name of the thing it is describing.

### Red Flag: Implementation Documentation Contaminates Interface

> This red flag occurs when interface documentation, such as that for a method, describes implementation details that aren’t needed in order to use the thing being documented.

### Write comments first

Use comments as placeholders when programming (body of functions, function calls interfaces etc.)

### Conclusion

> When writing comments, try to put yourself in the mindset of the reader and ask yourself what are the key things he or she will need to know. If your code is undergoing review and a reviewer tells you that something is not obvious, don’t argue with them; if a reader thinks it’s not obvious, then it’s not obvious.

## Naming

### Red Flag: Hard to pick name

> If it’s hard to find a simple name for a variable or method that creates a clear image of the underlying object, that’s a hint that the underlying object may not have a clean design.

## Modifying code

> If you want to maintain a clean design for a system, you must take a strategic approach when modifying existing code. Ideally, when you have finished with each change, the system will have the structure it would have had if you had designed it from the start with that change in mind.

> **_If you’re not making the design better, you are probably making it worse._**

## Consistency

> Consistency is another example of the investment mindset. It will take a bit of extra work to ensure consistency: work to decide on conventions, work to create automated checkers, work to look for similar situations to mimic in new code, and work in code reviews to educate the team. The return on this investment is that your code will be more obvious. Developers will be able to understand the code’s behavior more quickly and accurately, and this will allow them to work faster, with fewer bugs.

## Other redflags

### Red flag: Non-obvious code

> If the meaning and behavior of code cannot be understood with a quick reading, it is a red flag. Often this means that there is important information that is not immediately clear to someone reading the code.

### Software trends

#### OOP

> Before using implementation inheritance, consider whether an approach based on composition can provide the same benefits. For instance, it may be possible to use small helper classes to implement the shared functionality. Rather than inheriting functions from a parent, the original classes can each build upon the features of the helper classes.

### Agile

> One of the risks of agile development is that it can lead to tactical programming. Agile development tends to focus developers on features, not abstractions, and it encourages developers to put off design decisions in order to produce working software as soon as possible.

> Developing incrementally is generally a good idea, but the increments of development should be abstractions, not features. It’s fine to put off all thoughts about a particular abstraction until it’s needed by a feature. Once you need the abstraction, invest the time to design it cleanly; follow the advice of Chapter 6 and make it somewhat general-purpose.

### TDD

> Although I am a strong advocate of unit testing, I am not a fan of test-driven development. The problem with test-driven development is that it focuses attention on getting specific features working, rather than finding the best design.

### Design patterns

> The greatest risk with design patterns is over-application. Not every problem can be solved cleanly with an existing design pattern; don’t try to force a problem into a design pattern when a custom approach will be cleaner. Using design patterns doesn’t automatically improve a software system; it only does so if the design patterns fit.

### Conclusion

> Whenever you encounter a proposal for a new software development paradigm, challenge it from the standpoint of complexity: does the proposal really help to minimize complexity in large software systems? Many proposals sound good on the surface, but if you look more deeply you will see that some of them make complexity worse, not better.

## Performance

> Complicated code tends to be slow because it does extraneous or redundant work. On the other hand, if you write clean, simple code, your system will probably be fast enough that you don’t have to worry much about performance in the first place. In the few cases where you do need to optimize performance, the key is simplicity again: find the critical paths that are most important for performance and make them as simple as possible.

> Premature optimization is mother of all evil

[Someone @somewhere](https://google.com)


# The Pragmatic Programmer - D. Thomas & A. Hunt

## Software Entropy

### Don't live with broken windows

> . Ignoring a clearly broken
situation reinforces the ideas that perhaps nothing can be fixed, that no one cares, all is doomed; all negative thoughts which can spread among team members, creating a vicious spiral.


## Good-enough software

> Great software today is often preferable to the fantasy of perfect software tomorrow. If you give your users something to play with early, their feedback will often lead you to a better eventual solution.


## Invest regularly in your knowledge portfolio

> The more technologies you are comfortable with, the better you will be able to adjust to change. And don’t forget all the other skills you need, including those in nontechnical areas.


## Good design is easier to change than Bad design

> A thing is well designed if it adapts to the people who use it. For code, that means it must adapt by changing. So we believe in the ETC principle: ***Easier to Change***. ETC. 


## Design Principle - Orthogonality

> ***Eliminates Effects between unrelated things.***

***Orthogonality*** promotes predictability and code modules re-use. They can be assembled in a new predictible and easy to understand fashion.

### Benefits

#### Productivity gain

> Changes are localized, so development time and testing time are reduced. It is easier to write relatively small, self-contained components than a single large block of code. Simple components can be designed, coded, tested, and then forgotten—there is no need to keep changing existing code as you add new code.

> An orthogonal approach also promotes reuse. If components have specific, well-defined responsibilities, they can be combined with new components in ways that were not envisioned by their original implementors. 

> You get more functionality per unit effort by combining orthogonal components.

#### Risk Reduction

> Diseased sections of code are isolated. If a module is sick, it is less likely to spread the symptoms around the rest of the system. It is also easier to slice it out and transplant in something new and healthy.

> The resulting system is less fragile. Make small changes and fixes to a particular area, and any problems you generate will be restricted to that area.

> An orthogonal system will probably be better tested, because it will be easier to design and run tests on its components.

> You will not be as tightly tied to a particular vendor, product, or platform, because the interfaces to these third-party components will be isolated to smaller parts of the overall development.


## Design Principle - Reversibility

> Nothing is more dangerous than an idea if it’s the only one you have.

Alain - French motherfucker philosopher

> There are no final decisions (understand that the code is not cast in stone)


### Architectural Flexibility

>>> Good architecture doesn't just solve today's problem - it anticipates the possibility that today's perfect solution might be tomorrow's bottleneck. This means:
>>> - Creating proper abstractions around third-party services
>>> - Avoiding tight coupling with specific implementations
>>> - Treating major components as "pluggable" services


## Design Principle - Tracer Bullets

> Look for the important requirements, the ones that define the system. Look for the areas where you have doubts, and where you see the biggest risks. Then prioritize your development so that these are the first areas you code.

> Tracer development is consistent with the idea that a project is never finished: there will always be changes required and functions to add. It is an incremental approach.

> In a tracer code development, developers tackle use cases one by one. When one is done, they move to the next. It is far easier to measure performance and to demonstrate progress to your user. Because each individual development is smaller, you avoid creating those monolithic blocks of code that are reported as 95% complete week after week.

### Tracer coding vs Prototyping

> The tracer code approach addresses a different problem. You need to know how the application as a whole hangs together. You want to show your users how the interactions will work in practice, and you want to give your developers an architectural skeleton on which to hang code.


## Design Principle - Prototyping

> Prototypes are designed to answer just a few questions, so they are much cheaper and faster to develop than applications that go into production. The code can ignore unimportant details (unimportant to you at the moment, but probably very important to the user later on).

### Things to prototype

- Architecture
- New functionality in an existing system
- Structure of contents of external data
- Third-party tools or components
- Performance issues
- User interface design


### Architecture prototyping

- Are the responsibilities of the major areas well defined and appropriate?
- Are the collaborations between major components well defined?
- Is coupling minimized?
- Can you identify potential sources of duplication?
- Are interface definitions and constraints acceptable?
- Does every module have an access path to the data it needs during execution? Does it have that access when it needs it?

### Goal of prototyping

> It’s easy to become misled by the apparent completeness of a demonstrated prototype, and project sponsors or management may insist on deploying the prototype (or its progeny) if ***you don’t set the right expectations.***


## Design Principle - Estimating

### Iterate the Schedule with the Code

> So you complete the coding and testing of the initial functionality and mark this as the end of the first iteration. Based on that experience, you can refine your initial guess on the number of iterations and what can be included in each. The refinement gets better and better each time, and confidence in the schedule grows along with it. This kind of estimating is often done during the team’s review at the end of each iterative cycle.

> This may not be popular with management, who typically want a single, hard-and-fast number before the project even starts. You’ll have to help them understand that the team, their productivity, and the environment will determine the schedule.


## Fix the Problem, not the Blame

> It doesn’t really matter whether the bug is your fault or someone else’s. ***It is still your problem.***

> Read the Damn Error Message.


## Pragmatic Paranoia

> You Can’t Write Perfect Software.


### Design by Contract

> It is a simple yet powerful technique that focuses on documenting (and agreeing to) the rights and responsibilities of software modules to ensure program correctness.

> Here, the emphasis is on “lazy” code: be strict in what you will accept before you begin, and promise as little as possible in return. Remember, if your contract indicates that you’ll accept anything and promise the world in return, then you’ve got a lot of code to write!

> Simply enumerating what the input domain range is, what the boundary conditions are, and what the routine promises to deliver—or, more importantly, what it doesn’t promise to deliver—before you write the code is a huge leap forward in writing better software.


## Resources balancing

### Finish what you Start

> Most of the time, resource usage follows a predictable pattern: you allocate the resource, use it, and then deallocate it.

>>> Deallocate resources in the opposite order to that in which you allocate them. That way you won’t orphan resources if one resource contains references to another.
>>> When allocating the same set of resources in different places in your code, always allocate them in the same order. This will reduce the possibility of deadlock. (If process A claims resource1 and is about to claim resource2, while process B has claimed resource2 and is trying to get resource1, the two processes will wait forever.)

>>> If you are programming in an object-oriented language, you may find it useful to encapsulate resources in classes. Each time you need a particular resource type, you nstantiate an object of that class. When the object goes out of scope, or is reclaimed by the garbage collector, the object’s destructor then deallocates the wrapped resource.

```
thing = allocate_resource()
begin
	process(thing)
finally
	deallocate(thing)
end
```

## Tips

> - Don’t Chain Method Calls.
> - Avoid Global Data (You’ll find yourself writing a bunch of setup code to create a global environment just to allow your test to run.)
> - If It’s Important Enough to Be Global, Wrap It in an API
> - (...) stop what you’re doing. (...) Stop thinking about the code, and do something that is fairly mindless for a while, away from a keyboard.

## Configuration

> Parameterize Your App Using External Configuration (...) When code relies on values that may change after the application has gone live, keep those values external to the app. When your application will run in different environments, and potentially for different customers, keep the environment- and customerspecific values outside the app.

> We still want configuration data kept external to the application, but rather than in a flat file or database, we’d like to see it stored behind a service API.

## Patterns

### Finite State Machines

> It consists of a set of states, one of which is the current state. For each state, we list the events that are significant to that state. For each of those events, we define the new current state of the system.

> State machines are underused by developers, and we’d like to encourage you to look for opportunities to apply them.

### The Observer Pattern

> In the observer pattern we have a source of events, called the observable and a list of clients, the observers, who are interested in those events.

> But the observer pattern has a problem: because each of the observers has to register with the observable, it introduces coupling. In addition, because in the typical implementation the callbacks are handled inline by the observable, synchronously, it can introduce performance bottlenecks.

### Publish/Subscribe

> Publish/Subscribe (pubsub) generalizes the observer pattern, at the same time solving the problems of coupling and performance.

> In the pubsub model, we have publishers and subscribers. These are connected via channels. The channels are implemented in a separate body of code.

> Compared to the observer pattern, pubsub is a great example of reducing coupling by abstracting up through a shared interface (the channel). 

### Reactive Programming and Streams

> The current de facto baseline for reactive event handling is defined on the site http://reactivex.io, which defines a language-agnostic set of principles and documents some common implementations.


## Breaking Temporal Coupling / Concurrency and Parallelism

> Method A must always be called before method B; only one report can be run at a time; you must wait for the screen to redraw before the button click is received. Tick must happen before tock.

> We need to allow for concurrency and to think about decoupling any time or order dependencies. In doing so, we can gain flexibility and reduce any time-based dependencies in many areas of development: workflow analysis, architecture, design, and deployment.

> Analyze Workflow to Improve Concurrency (...) Activity diagrams show the potential areas of concurrency.

***See*** [Concurrency in UML 2.6](https://www.omg.org/certification/uml/documents/concurrency_in_uml_version_2.6.pdf)

> Random Failures Are Often Concurrency Issues.

### Semaphores

> A semaphore is simply a thing that only one person can own at a time. You can create a semaphore and then use it to control access to some other resource. 


## Don't program by coincidence

### Program delibetaretly

> - Always be aware of what you are doing
> - Can you explain the code, in detail, to a more junior programmer? If not, perhaps you are relying on coincidences.
> - Don’t code in the dark. Build an application you don’t fully grasp, or use a technology you don’t understand.
> - ***If you’re not sure why it works, you won’t know why it fails.***
> - ***Proceed from a plan.***
> - ***If you can’t tell if something is reliable, assume the worst.***
> - Document your assumptions.
> - Don’t just test your code, but test your assumptions as well. Don’t guess; actually try it.
> - Prioritize your effort. Spend time on the important aspects; more than likely, these are the hard parts.
> - Don’t let existing code dictate future code. All code can be replaced if it is no longer appropriate.

> So next time something seems to work, but you don’t know why, make sure it isn’t just a coincidence.

## Refactor Early, refactor Often

> - Don’t try to refactor and add functionality at the same time.
> - Make sure you have good tests before you begin refactoring. Run the tests as often as possible. That way you will know quickly if your changes have broken anything.
> - Take short, deliberate steps (...) If you keep your steps small, and test after each step, you will avoid prolonged debugging.


## Testing

> ***A Test is the First User of your Code***

> Test Your Software, or Your Users Will

> Design to Test.

### TDD cycles

> 1. Decide on a small piece of functionality you want to add.
> 2. Write a test that will pass once that functionality is implemented.
> 3. Run all tests. Verify that the only failure is the one you just wrote.
> 4. Write the smallest amount of code needed to get the test to pass, and verify that the tests now run cleanly.
> 5. Refactor your code: see if there is a way to improve on what you just wrote (the test or the function). Make sure the tests still pass when you’re done.

### Slaves to Test Driven Design

> - (Don't) spend inordinate amounts of time ensuring that they always have 100% test coverage.
> - (Don't do) redundant tests.

### Botom Up vs Top-Down

> Neither school actually works, because both ignore one of the most important aspects of software development: we don’t know what we’re doing when we start. The top-down folks  assume they can express the whole requirement up front: they can’t. The bottomup folks assume they can build a list of abstractions which will take them eventually to a single  top-level solution, but how can they decide on the functionality of layers when they don’t know where they are heading?

> By all means practice TDD. But, if you do, don’t forget to stop every now and then and look at the big picture. It is easy to become seduced by the green "tests passed" message, writing lots of code that doesn’t actually get you closer to a solution.

#### Build End-to-End, Not Top-Down nor Bottom-Up

> We strongly believe that the only way to build software is incrementally. Build small pieces of end-to-end functionality, learning about the problem as you go. Apply this learning as you continue to flesh out the code, involve the customer at each step, and have them guide the process.

### You need to know where you are going

> However, this approach can mislead you, encouraging you to focus on and endlessly polish the easy problems while ignoring the real reason you’re coding.

> Tests can definitely help drive development. But, as with every drive, unless you have a destination in mind, you can end up going in circles.

#### The cost of early rigidity

A More Pragmatic Approach to dumb TDD.

- Focus on critical path integration tests first
- Keep the code simple and malleable
- Avoid complex abstractions until patterns emerge
- Plan for refactoring when requirements stabilize

Over-tested, complex code early in a project can create:

- Fear of changes
- Analysis paralysis
- Maintenance burden
- False sense of security

### Unit testing

> We like to think of unit testing as testing against contract.

So, you can't have proper unit tests if you don't have proper contract.


# Domain Driven Design - Eric Evans

## TODO ...


# The Mythical Man-Month - 

> The tendency for managers to repeat such errors in project development led Brooks to quip that his book is called "The Bible of Software Engineering", because "everybody quotes it, some people read it, and a few people go by it".

[The Mythical Man Month @ Wikipedia](https://en.wikipedia.org/wiki/The_Mythical_Man-Month)

## TODO ...
