# Drupal Integrations

This project provides a composer plugin for placing commonly used shared
configuration files and scripts in desired locations inside Drupal project
directories.

Once installed, this project:

1. Installs [PHPStan][phpstan], [PHP_CodeSniffer][phpcs] and
   [Aikido Secrets pre-commit hook][aikidosecrets], along with the necessary
   configuration files and scripts to manage dependencies.
2. Creates a pre-commit script that runs linting, code quality and security
   related commands for every commit.
3. Updates the `.gitignore` file to ignore certain files.

[phpstan]: https://phpstan.org
[phpcs]: https://github.com/PHPCSStandards/PHP_CodeSniffer/
[aikidosecrets]: https://help.aikido.dev/ai-and-dev-tools/aikido-secrets-pre-commit-hook

## Requirements

[A `drupal/recommended-project` based Drupal project][drupal-recommended] is
required. Ensure your project has `drupal/core-composer-scaffold` and
`drupal/core-recommended` installed as well.

[drupal-recommended]: https://www.drupal.org/docs/develop/using-composer/manage-dependencies#s-create-a-project

## Installation

First, you need to update your `composer.json` file.

In your `repositories` section, create a new entry:

```json
{
  "repositories": {
     "drupal-integrations": {
        "type": "git",
        "url": "git@github.com:inan-hira/drupal-integrations.git"
     }
  }
}
```

Add an `allowed-packages` under `extra.drupal-scaffold" section, if it's not
there already, and list this repo:

```json
{
   "extra": {
      "allowed-packages": [
         "inan-hira/drupal-integrations"
      ]
   }
}
```

Finally, require this package by running:

```shell
composer require inan-hira/drupal-integrations
```

You can remove any duplicate requirements. This package will install:

1. `dealerdirect/phpcodesniffer-composer-installer`
2. `drupal/coder`
3. `mglaman/phpstan-drupal`
4. `phpstan/extension-installer`
5. `phpstan/phpstan`
6. `phpstan/phpstan-deprecation-rules`

## Installed tools

### PHPStan

PHPStan static analysis tool is installed. The scaffold also provides an initial
configuration file (`phpstan.neon`), which is basically a config that includes
your project's PHPStan file.

### PHP_CS

PHP_CodeSniffer, and fixer tool is installed, along with the `drupal/coder`
module, which provides [Drupal specific standards][drupal-coder]. The scaffold
provides a default `phpcs.xml` file.

[drupal-coder]: https://www.drupal.org/project/coder

### Aikido Local Scanner

[Aikido Local Scanner][aikidosecrets] is run as part of the pre-commit hook. The
`aikido-local-scanner` binary is required for the checks. This project provides
an installation script that checks your system for the binary, and installs it
if necessary.

> :warning: **Warning:**
> 
> Please note that the installed `aikido-local-scanner` binary is not the same
> tool as the [Aikido Local Code Scanning][aikido-scanner] tool, which
> confusingly uses the exact same name for its binary.

[aikido-scanner]: https://help.aikido.dev/code-scanning/local-code-scanning
