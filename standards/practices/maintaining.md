# Maintaining

## Summary
We maintain our code and keep it updated whenever Highland is working on it.

## Reasoning
1. Over time it becomes harder and harder to work with code that is reliant on outdated language and framework versions.
2. Keeping our software projects up to date mitigates the need to constantly be changing language and framework versions in development environments while moving between projects.
3. The longer updates go unaddressed, the harder they become to make.
4. Client's will almost never make code maintenance a priority, so we must. 

## Example/Instructions

### PHP & Laravel
* We use [Laravel Shift](https://laravelshift.com/) to assist in Laravel updates. 
  * Shift works by automatically updating Laravel and creating a PR with explanations and notes of any steps the developer may have to take.
  * Check out that branch, run the test suite, and review the app to make sure there are no problems.
  * Approve and merge the PR. 
* [Updating to PHP 8.0 with Laravel](https://blog.laravel.com/laravel-php-8-support)

## Exceptions
* We understand that this is sometimes not practical for legacy projects or ones that rely on brittle integrations.
* We strive to not create projects like this, but we understand it can happen.
* Developer discretion should take all factors into account before attempting updates.