# PART2

## SECTION4

good unit test suite:

1. It is integrated into the development cycle. You only get value from tests that you actively use;
   there’s no point in writing them otherwise.
2. It targets only the most important parts of your code base. Not all production code deserves
   equal attention. It’s important to differentiate the heart of the application (its domain model)
   from everything else.
3. It provides maximum value with minimum maintenance costs.

Regression is a software bug. It’s when a feature stops working as intended after some code
modification, usually after you roll out new functionality.

Bugs in business-critical functionality are the most damaging.

Test must include libraries, frameworks, and any external systems used in the project in the testing
scope, in order to check that the assumptions your software makes about these dependencies are
correct.

Resistance to refactoring—the degree to which a test can sustain a refactoring of the underlying
application code without failing.

The only way to reduce the chance of getting a false positive is to decouple the test from the
implementation details. You need to make sure the test verifies the end result the SUT delivers: its
observable behavior, not the steps it takes to do that. Tests should approach SUT verification from
the end user’s point of view and check only the outcome meaningful to that end user. Everything else
must be disregarded.

A test that couples to the SUT’s algorithm. Such a test expects to see one particular implementation
(the specific steps the SUT must take to deliver the result) and therefore is brittle. Any
refactoring of the SUT’s implementation would lead to a test failure.

Refactoring is changing the implementation without affecting the application’s observable behavior.

Keep as much distance as possible between the test and the code’s inner workings, and instead aim at
verifying the end result.

Four attributes of a good unit test:

1. Protection against regressions
2. Resistance to refactoring
3. Fast feedback
4. Maintainability

End-to-end tests provide great protection against both regression errors and false positives, but
they fail at the metric of fast feedback.

The best tests exhibit maximum maintainability and resistance to refactoring; always try to max out
these two attributes. The trade-off comes down to the choice between protection against regressions
and fast feedback.

End-to-end tests only make sense when applied to the most critical functionality.

End-to-end tests require the application to be hosted somewhere to fully emulate the end user, while
integration tests normally host the application in the same process.

![Ideal test](images/ideal_test.png)

![Pillars of Test](images/pillars_of_test.png)

![Test Pyramid](images/test_pyramid.png)

![Pyramid Choices](images/pyramid_choices.png)

Black-box testing examines the functionality of a system without knowing its internal structure.

White-box testing verifies the application’s inner workings. The tests are derived from the source
code, not requirements or specifications.

|   | Protection against regressions | Resistance to refactoring  |
| ------- | --- | --- |
| White-box testing | Good | Bad |
| Black-box testing | Bad | Good |

Choose black- box testing over white-box testing by default!

Use code coverage tools to see which code branches are not exercised, but then turn around and test
them as if you know nothing about the code’s internal structure. 