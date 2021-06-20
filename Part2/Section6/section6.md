# PART2

## SECTION6

Styles of unit testing:

- output-based
- state-based
- communication-based

Output-based testing is only applicable to code written in a purely functional way.

Functional programming is a method of programming that emphasizes a preference for side-effect-free
code.

The term state in this style of testing can refer to the state of the SUT itself, of one of its
collaborators, or of an out-of-process dependency, such as the database or the filesystem.

Communication-based testing uses mocks to verify communications between the system under test and
its collaborators.

The classical school of unit testing prefers the state-based style over the communication-based one.
The London school makes the opposite choice. Both schools use output- based testing.

Resistance to refactoring is the measure of how many false positives tests generate during
refactorings.

Comparing the styles using the metric of resistance to refactoring:
output-based > state-based > communication-based testing.

The vast majority of tests that check interactions with test doubles end up being brittle. This is
always the case for interactions with stubs—you should never check such interactions. Mocks are fine
only when they verify interactions that cross the application boundary and only when the side
effects of those interactions are visible to the external world.

Writing helper methods for tests is justified only when those methods are going to be reused across
multiple tests, which is rarely the case. (was mentioning for state-based testing)

Another way to shorten a state-based test is to define equality members in the class that is being
asserted. You could turn it into a value object (a class whose instances are compared by value and
not by reference).

Code pollution (polluting production code base with code whose sole purpose is to enable or, as in
this case, simplify unit testing). -> anti-pattern.

Two techniques—using helper methods and converting classes into value objects—are applicable only
occasionally. And even when these techniques are applicable, state-based tests still take up more
space than output-based tests and thus remain less maintainable.

Always prefer output-based testing over everything else.

Functional programming is programming with mathematical functions. A mathematical function produces
the same output for a given input regardless of how many times it is called.

An operation creates a side effect when it mutates the state of a class instance, updates a file on
the disk, and so on.

Determining whether a method is a mathematical function is to see if you can replace a call to that
method with its return value without changing the program’s behavior. The ability to replace a
method call with the corresponding value is known as referential transparency.

The goal of functional programming is not to eliminate side effects altogether but rather to
introduce a separation between code that handles business logic and code that incurs side effects.

Functional Architecture:

- Functional core (makes decision)
- Mutable shell (acts upon decision)
  Mutable shell should be as dumb as possible.

Quote from Michael Feathers:

- Object-oriented programming makes code understandable by encapsulating moving parts. Functional
  programming makes code understandable by minimizing moving parts.

Functional architecture pushes all side effects out of the immutable core to the edges of a business
operation. These edges are handled by the mutable shell. On the other hand, the hexagonal
architecture is fine with side effects made by the domain layer, as long as they are limited to that
domain layer only.

Functional architecture is a subset of the hexagonal architecture. You can view functional
architecture as the hexagonal architecture taken to an extreme.

Tests working directly with the filesystem don’t fit the definition of a unit test. They don’t
comply with the 2. (does it quickly) and the 3. (does it in isolation from other tests)
attributes of a unit test, thereby falling into the category of integration tests.

Only legitimate use case for mocking when it’s part of the application’s observable behavior.

You could embed errors into the method’s signature:

```
public (FileUpdate update, Error error) AddRecord(
FileContent[] files,
string visitorName,
DateTime timeOfVisit)
```

The application service would then check for this error. If it was there, the service wouldn’t pass
the update instruction.

A dependency on the database (for example simple query) introduces a hidden input to Class. Such a
class is no longer purely functional, and the whole application no longer follows the functional
architecture.

In most cases, you’ll have a combination of output-based and state-based styles, with a small mix of
communication-based tests, and that’s fine.

Functional architecture concedes performance for maintainability gains.

Not all code bases are worth converting into functional architecture. 