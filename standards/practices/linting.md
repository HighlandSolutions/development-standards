# Linting
## Summary
We lint our code.


## Reasoning
1. Consistent formatting is easier to read than inconsistent formatting.
2. Linting helps us avoid errors.
3. Linting reduces noise from functionally meaningless changes as seen in diffs.


## Example/Instructions
For all languages, enable extensions' fix-on-save options (or at least fix warnings/errors in your code before submitting for peer review).

### JavaScript
#### One-time setup
Install an editor extension. Here are some popular options:

- [Atom](https://atom.io/packages/linter-eslint)
- [Brackets](https://github.com/fdecampredon/brackets-eslint)
- [Sublime Text](https://packagecontrol.io/packages/SublimeLinter-eslint)
- [VS Code](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

#### Project setup
Run from project root:  

```sh
npm i -D eslint @highlandsolutions/eslint-config-highland
curl https://raw.githubusercontent.com/HighlandSolutions/development-standards/main/assets/linting/.eslintrc.js > .eslintrc.js
```

Tweak `.eslintrc.js` as needed. For example, you might need to enable linting for Vue, add a global, or tweak import resolution.

### PHP
#### One-time setup
Install PHP Coding Standards Fixer.

```sh
brew install php-cs-fixer
```

Install an editor extension. Here are some popular options:

- [Atom](https://atom.io/packages/php-cs-fixer)
- [Sublime Text](https://packagecontrol.io/packages/SublimeLinter-contrib-php-cs-fixer)
- [VS Code](https://marketplace.visualstudio.com/items?itemName=junstyle.php-cs-fixer)

#### Project setup
Run from project root:

```sh
composer require --dev friendsofphp/php-cs-fixer
curl https://raw.githubusercontent.com/HighlandSolutions/development-standards/master/assets/linting/.php-cs-fixer.php > .php-cs-fixer.php
```
