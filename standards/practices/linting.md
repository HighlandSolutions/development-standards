# Title
## Summary
We lint our code.


## Reasoning
1. Consistent formatting is easier to read than inconsistent formatting.
2. Linting helps us avoid errors.


## Example/Instructions
1. Install a linter for each language used in your project.
    - PHP
      ```sh
      brew install php-code-sniffer
      ```
    - JavaScript
      ```sh
      yarn add -D eslint
      ```
2. Install editor extensions for the linters. Here are some popular options:
    - Atom
      - https://atom.io/packages/linter
      - https://atom.io/packages/linter-eslint
      - https://atom.io/packages/linter-phpcs
    - Sublime Text
      - https://packagecontrol.io/packages/SublimeLinter
      - https://packagecontrol.io/packages/SublimeLinter-eslint
      - https://packagecontrol.io/packages/SublimeLinter-phpcs
    - VS Code
      - https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint
      - https://marketplace.visualstudio.com/items?itemName=ikappas.phpcs
3. Fix warnings/errors in your code before submitting for peer review.
