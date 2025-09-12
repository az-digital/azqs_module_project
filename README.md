# Quickstart website custom module composer project template

This repo provides a composer project template for creating a custom Drupal
module designed to be used on Arizona Quickstart websites but that is not
suitable for inclusion in Quickstart itself for one reason or another.

## Table of Contents
- [Create project from this template repository](#create-project-from-this-template-repository)
- [Where to replace the module name](#where-to-replace-the-module-name)
- [Add repository as VCS in a consuming site](#add-repository-as-vcs-in-a-consuming-site)
- [Drush availability](#drush-availability)
- [Forking / namespace guidance](#forking--namespace-guidance)
- [Changing registry root / namespace in Lando](#changing-registry-root--namespace-in-lando)
- [Lando configuration](#lando-configuration)
## Create project from this template repository
To create your own module project using this repository as a template use the
following composer command:
```
composer create-project --no-install --ask az-digital/azqs_module_project:dev-main
```

After creating your project, you'll want to replace all instances of
`azqs_module_project` and `azqs-module-project` with your own module name.

## Where to replace the module name
Occurrences (search and replace both snake_case and dashed forms):
- `composer.json` -> name: `az-digital/azqs_module_project`
- `.lando.yml` -> name: `azqs-module-project`, volume paths `/usr/local/azqs-module-project`
- `.lando.yml` -> composer require line: `az-digital/azqs_module_project` and path reference
- `.lando.yml` -> drush install task `pm:install -y azqs_module_project`
- `.lando.yml` -> phpcs/phpcbf/phpstan commands referencing `web/modules/custom/azqs_module_project`
- Any README examples (this file)

## Add repository as VCS in a consuming site
If your module is NOT published on Packagist, add it as a path or VCS repository in the consuming site's `composer.json`:
```jsonc
// In the consuming site's composer.json
{
	"repositories": [
		{ "type": "vcs", "url": "git@github.com:your-org/your-module.git" }
	]
}
```
Then require it (adjust version constraint as needed):
```
composer require your-org/your-module:dev-main
# Arizona Quickstart Custom Module Template – Step‑by‑Step Guide

Use these steps to turn this template into a working custom module repository for an Arizona Quickstart site.

---
## 1. Create a project from this template
```
composer create-project --no-install --ask az-digital/azqs_module_project:dev-main your_module_dir
cd your_module_dir
```

## 2. Pick your module names
Decide on:
- Machine name (snake case): e.g. `awesome_feature_module`
- Dashed name: `awesome-feature-module`
- Human name: `Awesome Feature Module`

## 3. Global search & replace
Replace everywhere (case sensitive):
- `azqs_module_project` → `awesome_feature_module`
- `azqs-module-project` → `awesome-feature-module`

Files to check:
- `composer.json` (package name)
- `.lando.yml` (project name, volume path, composer require line, Drush install line, tooling paths)
- Any README references

Then update `composer.json` "name":
```
"name": "your-namespace/awesome_feature_module"
```

## 4. (Optional) Fork or template
If you forked, rename the repo to your module machine name. If you used “Use this template”, push the new repo to your org/user namespace. Transfer later to `az-digital` if it becomes shared.

## 5. Require dependencies
Install the scaffold (if not already from Lando build) and module dependencies:
```
composer install
```

## 6. Add to a consuming site (if private / not on Packagist)
In the consuming site’s `composer.json` add:
```jsonc
{
	"repositories": [
		{ "type": "vcs", "url": "git@github.com:your-org/awesome_feature_module.git" }
	]
}
```
Then require it:
```
composer require your-org/awesome_feature_module:dev-main
```
Local path alternative during development:
```jsonc
{
	"repositories": [
		{"type": "path", "url": "../awesome_feature_module", "options": {"symlink": true}}
	]
}
```

## 7. Start Lando environment
```
lando start
lando install
```

## 8. Verify Drush
```
lando drush status
```
If missing:
```
composer require drush/drush --dev
```

## 9. Enable your module in the site (if not auto‑installed)
```
lando drush en awesome_feature_module -y
```

## 10. Code quality & static analysis
```
lando phpcs
lando phpcbf   # to auto-fix
lando phpstan  # static analysis
```

## 11. Rewrite this README for your module
Replace template language with real module documentation. Suggested sections:
- Overview (what problem it solves)
- Features (bulleted)
- Installation (any steps beyond enabling)
- Configuration (forms, permissions, settings)
- Development (coding standards, tests, local setup notes)
- Maintainers / Support

Remove leftover template-specific guidance.

## 12. Commit your initialized module
```
git add .
git commit -m "Initialize Awesome Feature Module from template"
git push origin main
```

## 13. Checklist before sharing
- No remaining `azqs_module_project` or `azqs-module-project`
- Composer package name updated
- Lando commands run successfully
- Module installs & enables with Drush
- Coding standards pass or are fixable (`phpcbf`)
- Static analysis passes with acceptable level

## 14. Next steps
- Add a proper description of the module’s functionality.
