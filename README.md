# Arizona Quickstart Module Template

The fastest way to create a new module for use in an Arizona Quickstart site.

## 1. Create project
```
composer create-project --no-install --ask az-digital/azqs_module_project:dev-main awesome_feature_module
cd awesome_feature_module
```

## 2. Rename
Replace these two strings in all files:
- `azqs_module_project` → `awesome_feature_module`
- `azqs-module-project` → `awesome-feature-module`

Files to update:
- `azqs_module_project.info.yml` (rename file)  to `awesome_feature_module.info.yml`)
- `composer.json` (change `az-digital/azqs_module_project` to `YOUR_ORG/awesome_feature_module`)
- `.lando.yml` (change `az-digital/azqs_module_project` to `YOUR_ORG/awesome_feature_module` and update other references)

## 3. Start & install
```
lando start
lando install
lando drush status
```

## 4. Rewrite README
Replace this README with real module documentation (overview, features, install, config, maintainer info).

## 5. Run code quality checks & fixes
```
lando phpcs
lando phpcbf
lando phpstan
```

## 6. Push to new GitHub repo
```
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:YOUR_ORG/awesome_feature_module.git
git push -u origin main
```
