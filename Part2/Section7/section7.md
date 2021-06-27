# PART2

## SECTION7

All production code can be categorized along two dimensions:

1. Complexity or domain significance
2. The number of collaborators

It’s better to delegate all communications with out-of-process dependencies to classes outside the
domain layer. The domain classes then will only work with in-process dependencies.

Fat Controllers don’t delegate complex work anywhere and do everything themselves.

The general idea is to split overcomplicated code into two parts: algorithms and controllers.

The more important or complex the code, the fewer collaborators it should have.

100% coverage shouldn’t ever be your goal. Your goal is a test suite where each test adds
significant value to the project.

Your code can be either deep (complex or important) or wide (work with many collaborators), but
never both.

Affirmative statements are more readable than negative ones.

All side effects are contained in memory until the very last moment improves testability a lot.

The Humble Object pattern helps make overcomplicated code testable by extracting business logic out
of that code into a separate class.

When you need to refer to out-of-process dependencies in the middle of the business operation:
![When business logic get complex](https://raw.githubusercontent.com/furkantopal/unit-testing-notes/main/images/when_business_logic_get_complex.png)

The CanExecute/Execute pattern essentially eliminates the controller’s decision-making because
there’s no option not to call CanDo() before Do().

Domain events should always be named in the past tense because they represent things that already
happened. 