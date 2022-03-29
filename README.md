# Quickstart module composer project template

This repo provides a composer project template for creating a custom Drupal
module designed to be used on Arizona Quickstart website but that is not
suitable for inclusion in Quickstart itself for one reason or another.

## Create project from this template repository
To create your own module project using this repository as a template use the
following composer command:
```
composer create-project --no-install --ask az-digital/azqs_module_project:dev-main
```

After creating your project, you'll want to replace all instances of
`azqs_module_project` and `azqs-module-project` with your own module name.

## Lando configuration
This project template includes a sample lando configuration file that can be
used to automatically build a local Arizona Quickstart site with your module
installed for development and testing.
```
lando start
lando install
```

The sample lando configuration also includes tooling that expose Quickstart's
code quality tools for checking that your module code adhere's to Quickstart's
coding standards.
```
lando phpcs

lando phpcbf

lando phpstan
```
