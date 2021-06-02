# PART1

## SECTION3

3A pattern.

1. In the arrange section, you bring the system under test (SUT) and its dependencies to a desired
   state.
2. In the act section, you call methods on the SUT, pass the prepared dependencies, and capture the
   output value (if any).
3. In the assert section, you verify the outcome. The outcome may be represented by the return
   value, the final state of the SUT and its collaborators, or the meth- ods the SUT called on those
   collaborators.

(given / when / then) = (arrange / act / assert)

In TDD start with assert otherwise arrange.

When you see multiple act sections separated by assert and, possibly, arrange sections, it means the
test verifies multiple units of behavior. And, such a test is no longer a unit test but rather is an
integration test.

Multiple arrange, act, and assert sections are a hint that the test verifies too many things at
once. Such a test needs to be split into several tests to fix the problem.

If statement in unit and integration test is an anti-pattern. There is be no branching. An if
statement indicates that the test verifies too many things at once. Such a test, therefore, should
be split into several tests.

Arrange section can be the largest one.As much as sum of act and assert sections. If arrange section
is so much bigger than sum of these two section, then it's better to think other approaches such as:
Object mother and Test data builder.

The act section is normally just a single line of code. If the act consists of two or more lines, it
could indicate a problem with the SUT’s public API. The act of protecting your code against
potential inconsistencies is called encapsulation. Keeping the act section down to a single line
holds true for the vast majority of code that contains business logic, but less so for utility or
infrastructure code. Thus, I won’t say “never do it.” Be sure to examine each such case for a
potential breach in encapsulation, though.

A single unit of behavior can exhibit multiple outcomes, and it’s fine to evaluate them all in one
test.but need to watch out for assertion sections that grow too large.

Teardown can be used for to remove any files created by the test, close a database connection, and
so on. The teardown is usually represented by a separate method, which is reused across all tests in
the class. Note that most unit tests don’t need teardown. Unit tests don’t talk to out-of-process
dependencies and thus don’t leave side effects that need to be disposed of. That’s a realm of
integration testing.

Always name the SUT in tests sut. var sut = new Calculator(); The calculator is now called sut.

Put // Arrange, // Act, and // Assert comments before the beginning of each section.
(or empty line)

Each test should tell a story. A higher-level description of the application’s behavior.

A test fixture is an regular dependency, an argument that is passed to the SUT. It can also be data
in the database or a file on the hard disk.

Constructor in test class run after each test in the class.

High coupling between tests is an anti-pattern.

A modification of one test should not affect other tests. We are talking about independent
modification of tests, not independent execution. Avoid introducing shared state in test classes.

Extracting the arrangement code into the constructor is diminished test readability.

To reuse text fixture introduce private factory methods. By extracting the common initialization
code into private factory methods. You can instantiate a fixture in the constructor if it’s used by
all or almost all tests. This is often the case for integration tests that work with a database. All
such tests require a database connection, which you can initialize once and then reuse everywhere.
But even then, it would make more sense to introduce a base class and initialize the database
connection in that class’s constructor, not in individual test classes.

Naming convention: description of the behaviour under test in plain English. Name the test as if you
were describing the scenario to a non-programmer who is familiar with the problem domain. Separate
words with underscores.

Using the pattern [ClassName]Tests when naming test classes, it doesn’t mean the tests are limited
to verifying only that class. Remember, the unit in unit testing is a unit of behavior, not a class.
This unit can span across one or several classes; the actual size is irrelevant. It is just an entry
point.

Don’t include the name of the SUT’s method in the test’s name. While naming “should_be” is a
anti-pattern. There’s no place for a wish or a desire when stating a fact.

Parameterized tests is an important notion, check the implementation. While using parametrized
tests, grouping as positive and negative would be better. AssertJ: fluent assertion Java library. 
