# PART1

## SECTION2

Two style: classic(Detroit) vs London(mockist): main difference is about isolation.

Test double notion is important. One benefit of London approach is that if the test fails, you know
for sure which part of the code base is broken: it’s the system under test. (because of mocks and
test doubles, there is no an other suspect)

Have a class? Create a corresponding class with unit tests!

three-phase sequence: arrange, act, and assert (AAA for short)
arrange phase -> SUT (system under test) and collaborator. MUT (method under test) is the method the
SUT calls. SUT != MUT In Java world, you can use Mockito, JMock, or EasyMock.

Mocks are a subset of test doubles. People often use the terms test double and mock as synonyms, but
technically, they are not.

With mock instead of modifying the state of an object, we tell the mock how to respond.

Mocking the interface instead of class. Mocking a class is an anti-pattern.

With mock in assert part, instead of asserting against object state, checking if objects method
correctly called.

Here are all the attributes of a unit test once again:

1. A unit test verifies a small piece of code (a unit),
2. Does it quickly,
3. And does it in an isolated manner.

Shared dependency: database is example.

Usually use mocks for only those dependencies that introduce a shared state between tests.

A singleton dependency is not shared as long as you are able to create a new instance of it in each
test.

The London school views it as isolation of the system under test from its collaborators, whereas the
classical school views it as isolation of unit tests themselves from each other.

Tests shouldn’t verify units of code. Rather, they should verify units of behavior. The number of
classes it takes to implement such a unit of behavior is irrelevant. The unit could span across
multiple classes or only one class, or even take up just a tiny method.

And so, aiming at better code granularity isn’t helpful. As long as the test checks a single unit of
behavior, it’s a good test. Targeting something less than that can in fact damage your unit tests,
as it becomes harder to understand exactly what these tests verify. A test should tell a story about
the problem your code helps to solve, and this story should be cohesive and meaningful to a
non-programmer.

Instead of finding ways to test a large, complicated graph of interconnected classes, you should
focus on not having such a graph of classes in the first place. More often than not, a large class
graph is a result of a code design problem.

Test-driven development

1. Write a failing test to indicate which functionality needs to be added and how it should behave.
2. Write just enough code to make the test pass. At this stage, the code doesn’t have to be elegant
   or clean.
3. Refactor the code. Under the protection of the passing test, you can safely clean up the code to
   make it more readable and maintainable.

Point of view of the classical school. A unit test is a test that

1. Verifies a single unit of behavior,
2. Does it quickly,
3. And does it in isolation from other tests.

Even if the test works with hundreds of in-memory objects, the communication with them will still
execute faster than a call to a database.

A test is an integration test when it verifies two or more units of behavior.

End-to-end tests normally include all or almost all out-of-process dependencies in the scope.
Integration tests check only one or two such dependencies—those that are easier to set up
automatically, such as the database or the file system.

