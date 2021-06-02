# PART1

## SECTION1

Unit testing practices lead to a better design.

The poor quality usually manifests itself in tight coupling, which means different pieces of
production code are not decoupled from each other enough, and it’s hard to test them separately.

Consider thinking about low coupling high cohesion again.

You can’t achieve the goal of unit testing by just throwing more tests at the project. You need to
consider both the test’s value and its upkeep cost. The cost component is determined by the amount
of time spent on various activities:

1. Refactoring the test when you refactor the underlying code
2. Running the test on each code change
3. Dealing with false alarms raised by the test
4. Spending time reading the test when you’re trying to understand how the underlying code behaves

The common belief is that the higher the coverage number, the better. Unfortunately, it’s not that
simple, and coverage metrics, while providing valuable feedback, can’t be used to effectively
measure the quality of a test suite. It’s the same situation as with the ability to unit test the
code: coverage metrics are a good negative indicator but a bad positive one.

There are two coverage techniques: code coverage ve branch coverage.

NO COVERAGE METRIC CAN TAKE INTO ACCOUNT CODE PATHS IN EXTERNAL LIBRARIES.

In most applications, the most important part is the part that contains business logic.

Each time you change something in a code base, the amount of disorder in it, or entropy, increases.
All tests are not created equal. 
