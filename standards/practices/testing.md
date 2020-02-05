# Testing
## Summary
We test our code with as few tests as possible to provide reasonable confidence our software functions as intended.


## Reasoning
Testing is an essential part of software development. More specifically it:

- proves our code works,
- reduces the risk of creating regression bugs,
- is essential for CI/CD, and
- documents our design.


## Example/Instructions
Write [unit](#unit-tests), [integration](#integration-tests), and [acceptance](#acceptance-tests) tests that:

- serve the above reasons and
- people can easily read and understand.

For the following examples, consider the following code:

```php
<?php

namespace App\Library\Helpers;

use App\User;

class AuthHelper
{   
    /**
     * Determine which auth provider to use.
     *
     * @param string $email
     * @return string
     */
    public function getAuthProviderKey($email)
    {
        return $this->adminUserExists($email) ? 'admin-users' : 'client-users';
    }

    /**
     * Check if an admin user with the provided email address exists.
     *
     * @param string $email
     * @return bool
     */
    private function adminUserExists($email)
    {
        return User::where('email', $email)->count() > 0;
    }
}
```

**Bad**
```php
<?php

namespace Tests\Unit;

use App\ClientUser;
use App\User;
use Facades\App\Library\Helpers\AuthHelper;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Tests\TestCase;

class AuthHelperTest extends TestCase
{
    use RefreshDatabase;
    
    function testUsersReturnsAdminUsersButClientUsersReturnsClientUsers()
    {    
        $this->assertEquals('client-users', AuthHelper::getAuthProviderKey(factory(User::class)->create()->email));
        $this->assertEquals('admin-users', AuthHelper::getAuthProviderKey(factory(ClientUser::class)->create()->email));
    }
}
```

This test is bad for a number of reasons:

1. It's supposed to be a [unit test](#unit-tests), but it depends on outside systems (the database and User model).
2. One test covers two different actions.
3. The test name is difficult to read in camelCase.
4. The test mixes all stages together.
5. The code covered is so simple it's not worth testing (little more than third-party code hidden behind a simple ternary).

**Good**
```php
<?php

namespace Tests\Feature;

use App\ClientUser;
use App\User;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Tests\TestCase;

class AuthenticationTest extends TestCase
{
    use RefreshDatabase;

    /** @test */
    public function admins_can_log_in()
    {
        // Arrange
        // Create an admin.
        $user = factory(User::class)->create(['password' => bcrypt('pw1234')]);

        // Act
        // Try to log in.
        $response = $this->post('/login', [
            'email'    => $user->email,
            'password' => 'pw1234'
        ]);

        // Assert
        // Ensure user logged in.
        $response->assertRedirect(route('home'));
        $this->assertAuthenticatedAs($user);
    }

    /** @test */
    public function client_users_can_log_in()
    {
        // Arrange
        // Create a client user.
        $user = factory(ClientUser::class)->create(['password' => bcrypt('pw1234')]);

        // Act
        // Try to log in.
        $response = $this->post('/login', [
            'email'    => $user->email,
            'password' => 'pw1234'
        ]);

        // Assert
        // Ensure user logged in.
        $response->assertRedirect(route('home'));
        $this->assertAuthenticatedAs($user);
    }
}
```

*In most frameworks, it's not worth testing authentication, because the framework handles pretty much everything. However in this example, the authentication is customized enough that we need to avoid regressions.*

These two tests improve on the previous example in several ways:

1. We converted from a unit test to an integration test (called a feature test in Laravel). The feature depends on several systems more simply tested with a couple short integration tests than with several unit tests that can't reliably test the whole feature.
2. Each test covers only one action.
3. We formatted the test names so people can easily read it and understand what it tests.
4. Each test is split into the standard arrange, act, and assert steps with helpful explanations.
5. The tests cover complex functions likely affected by regressions.


## Explanation
Tests help us improve the quality of our software. However, tests carry maintenance costs, so **our tests should add value to our software**. In pursuit of this value:

1. **Avoid overly-specific coverage goals.**  
  E.g. 80% code coverage. Goals like this incentivize writing more tests than required to obtain confidence in the software.
2. **Don't test what you don't own.**  
  Testing languages, frameworks, and other third-party software indicates you don't trust the dependency you decided to rely on.
3. **Avoid testing basic operations.**  
  E.g. Testing an Eloquent model's relationships. Though you own the method on the model, in nearly every case, it merely consumes the framework.
4. **Test the input and output, not the implementation.**  
  Implemtation may change over time. Tests shouldn't fail after refactoring.

Breaking these guidelines usually adds to maintenance costs without adding worthwhile value to our software.

### Unit tests
*Test individual pieces of code.*

Unit tests verify a relatively small piece of code is doing what it's intended to do. They shouldn’t have dependencies on outside systems, because they test internal consistency, not that units play nicely with outside systems.

#### When (not) to use
Write unit tests for non-trivial pieces of isolated code or to help you break integration tests into manageable steps.

Avoid writing setup-heavy unit tests, because they're brittle. If you find yourself writing a unit test that requires complex mocking or requires significantly more code than the covered function, you should most likely use an integration test instead or rethink your implementation. Mocking tightly couples code to tests, which prevents proper refactoring (improving code without changing tests).

### Integration Tests
*Test the integrations of many units together (dependencies, databases and libraries).*

Integration tests demonstrate that different pieces of the system work together. They are more convincing than unit tests, assuming the test environment resembles production.

#### When (not) to use
Write integration tests for things like ensuring a request to an endpoint returns the correct response.

Avoid writing integration tests to replace unit testing a function with several different logic branches (like switch statements).

### Acceptance Tests
*Test that the program works when a user interacts with it.*

Acceptance tests make sure a feature is correctly implemented. They're similar to integration tests, but more focused on the use case and generally run in a browser.

#### When (not) to use
Write acceptance tests to cover crucial user operations (which sometimes rely on JavaScript).

Avoid writing acceptance tests that cover trivial features or require a lot of specific page configurations. For example, when the client decides to change some text, you should be able to update it without updating a bunch of tests.
