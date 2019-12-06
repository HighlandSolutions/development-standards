# Testing
## Summary
Testing is an essential part of software development and part of Highland Solutions' culture.

However, tests carry a maintenance weight, just like production code. We should make sure that the tests we write add value to our systems. We should avoid testing things like "1+1=2" or configuring our framework. Testing production paths multiple times should also be avoided.


## Reasoning
* It lets us know our code works.
* It helps us reduce the risk of creating regression bugs.
* It is essential for CI/CD.
* It documents our design.


## Example/Instructions
### Unit tests
"Test each individual piece of code"

A unit test is a test written by a programmer to verify that a relatively small piece of code is doing what it is intended to do. Unit tests shouldn’t have dependencies on outside systems. They test internal consistency as opposed to proving that they play nicely with some outside system. 

We should strive to test all the branches of a function. However, when you create setup-heavy tests, you create brittle tests. If you find yourself writing a unit test that requires lots of complex mocking or uses 10x more code than the function being tested, then you need to use an integration test instead (or redesign your function).

### Integration Tests
"Test the integrations of many units together (dependencies, databases and libraries)"

An integration test is done to demonstrate that different pieces of the system work together. The integration tests do a more convincing job of demonstrating the system works (especially to non-programmers) than a set of unit tests can, at least to the extent the integration test environment resembles production.

We should find a happy balance between unit/integration/acceptance tests. Integration tests should be used for things like making sure a route calls a controller function, queries a database properly and returns the correct response. It shouldn't be used to replace unit testing a function that has lots of different logic branches.

### Acceptance Tests
"Test that the program works the way a user/customer expects"

Acceptance tests make sure a feature or use case is correctly implemented. It is similar to an integration test, but with a focus on the use case rather than on the components involved.

Acceptance tests are useful for covering your CRUD operations and frontend (JavaScript) logic. Avoid writing acceptance tests that require a lot of specific page configurations. For example clients like to change text often, and developers should be able to make a text update without having to rewrite a bunch of tests.
