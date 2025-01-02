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

Unit Testing: Testing individual units or components of code in isolation to ensure their correctness.
Integration Testing: Testing the interaction between multiple components to ensure they work together as expected.
Functional Testing: Testing the software's functionality against the requirements.
Regression Testing: Ensuring that new code changes do not break existing functionality.

