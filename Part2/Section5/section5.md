# PART2

## SECTION5

There’s a deep and almost inevitable connection between mocks and test fragility.

Test double types:

1. mocks (mock, spy)
2. stubs (stub, dummy, fake)

- Mock-> outcoming interactions
- Stub-> incoming interactons


- Sending an email is an outcoming interaction: an interaction that results in a side effect in the
  SMTP server. A test double emulating such an interaction is a mock.
- Retrieving data from the database is an incoming interaction; it doesn’t result in a side effect.
  The corresponding test double is a stub.

Spies are written manually, whereas mocks are created with the help of a mocking framework.
Sometimes people refer to spies as handwritten mocks.

You can use a mock (the tool) to create both types of test doubles: mocks and stubs.

*Mock example*

```
[Fact]
public void Sending_a_greetings_email()
{
var mock = new Mock<IEmailGateway>();
var sut = new Controller(mock.Object);
sut.GreetUser("user@email.com");
mock.Verify(
x => x.SendGreetingsEmail(
"user@email.com"),
Times.Once);
}
```

*Stub example*

```
[Fact]
public void Creating_a_report()
{
var stub = new Mock<IDatabase>();
stub.Setup(x => x.GetNumberOfUsers())
.Returns(10);
var sut = new Controller(stub.Object);
Report report = sut.CreateReport();
Assert.Equal(10, report.NumberOfUsers);
}
```

Asserting interactions with stubs is a common anti-pattern that leads to fragile tests.

Verifying things that aren’t part of the end result is also called over-specification. Checking for
interactions with stubs is a flaw that’s quite easy to spot because tests shouldn’t check for any
interactions with stubs.

**CQS(Command Query Separation)**

- if method has side effect, should return void.
- if method returns value, should stay side-effect free.

Commands correspond to mocks, while queries are consistent with stubs.

```
var mock = new Mock<IEmailGateway>();
mock.Verify(x => x.SendGreetingsEmail("user@email.com"));

var stub = new Mock<IDatabase>();
stub.Setup(x => x.GetNumberOfUsers()).Returns(10);
```

The only way to avoid such coupling is to verify the end result the code produces (its observable
behavior)
and distance tests from implementation details as much as possible.

If the number of operations the client has to invoke on the class to achieve a single goal is
greater than one, then that class is likely leaking implementation details.

By making all implementation details private, you leave your tests no choice other than to verify
the code’s observable behavior, which automatically improves their resistance to refactoring.

The separation of concerns between the application services layer and the domain layer means that
the former knows about the latter, but the opposite is not true. The domain layer should be fully
isolated from the external world.

The ability for tests to run in parallel, sequentially, and in any order is called test isolation.

If a shared dependency is not out-of-process, then it’s easy to avoid reusing it in tests by
providing a new instance of it on each test run. In cases where the shared dependency is
out-of-process, testing becomes more complicated. You can’t instantiate a new database or provision
a new message bus before each test execution; that would drastically slow down the test suite. The
usual approach is to replace such dependencies with test doubles—mocks and stubs.

![Observable vs Implementation](https://raw.githubusercontent.com/furkantopal/unit-testing-notes/main/images/observable_vs_implementation.png)

All production code can be categorized along two dimensions:

- public API versus private API,
- and observable behavior versus implementation details.

There are two types of communications in an application:

- intra-system and inter-system.

Mocking is legitimate only when it’s used for inter-system communications and only when the side
effects of those communications are visible to the external world.
