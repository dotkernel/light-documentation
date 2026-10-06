# Upgrading from 1.0 to 1.5

## Summary

The changes made to the Dotkernel Light skeleton between releases 1.0.0 and 1.5.0, split into updates that affect a project created from the skeleton and updates you can safely skip.

## Details

This page covers every release from 1.0.0 to 1.5.0 (1.0.1, 1.1.0, 1.1.1, 1.2.0, 1.3.0, 1.4.0 and 1.5.0), all published from the `1.0` branch of [dotkernel/light](https://github.com/dotkernel/light).
Version numbers on this page are the ones in `composer.json` and `package.json` at tag `1.5.0`.

Apply the changes to your own project by comparing it with the skeleton at tag `1.5.0`.

### Important updates

#### PHP versions

The supported PHP versions changed from `~8.2.0 || ~8.3.0` to `~8.3.0 || ~8.4.0 || ~8.5.0`.

- PHP 8.4 support was added in [#25](https://github.com/dotkernel/light/pull/25).
- PHP 8.5 support was added in [#68](https://github.com/dotkernel/light/pull/68).
- PHP 8.2 support was dropped in [#73](https://github.com/dotkernel/light/pull/73), which also upgrades PHPUnit from 10.5 to 12.5.23 and updates `phpunit.xml` and two tests.

If you run PHP 8.2, upgrade PHP before upgrading the skeleton.
If you have your own tests, they must run on PHPUnit 12.

#### Composer requirements

Two pull requests raise the framework requirements:

- [#29](https://github.com/dotkernel/light/pull/29) cleans up `composer.json`: it removes `friendsofphp/proxy-manager-lts` and raises the minimum version of most requirements.
- [#65](https://github.com/dotkernel/light/pull/65) raises `mezzio/mezzio` and `mezzio/mezzio-fastroute`.

The `require` block at tag `1.5.0`, which also reflects the changes described in the sections below:

```json
"require": {
    "php": "~8.3.0 || ~8.4.0 || ~8.5.0",
    "dotkernel/dot-errorhandler": "^5.0.0",
    "laminas/laminas-component-installer": "^3.5.0",
    "laminas/laminas-config-aggregator": "^1.17.0",
    "mezzio/mezzio": "^3.24.0",
    "mezzio/mezzio-fastroute": "^3.13.0",
    "mezzio/mezzio-twigrenderer": "^2.17.0"
}
```

`dotkernel/dot-controller` and `dotkernel/dot-twigrenderer` are no longer required.
Both are covered below.

#### Composer scripts

- [#9](https://github.com/dotkernel/light/pull/9) replaces Psalm with PHPStan.
  It removes `psalm.xml`, adds `phpstan.neon` and adds `phpstan/phpstan`, `phpstan/phpstan-phpunit` and `symfony/var-dumper` to `require-dev`.
  The `static-analysis` script now runs PHPStan, at level 8 in `phpstan.neon`.
- [#20](https://github.com/dotkernel/light/pull/20) raises the PHPStan memory limit, so the script is now `phpstan analyse --memory-limit 1G`.
- [#37](https://github.com/dotkernel/light/pull/37) removes the `test-coverage` script.
- [#15](https://github.com/dotkernel/light/pull/15) adds `bin/composer-post-install-script.php` and a `post-update-cmd` script that runs it.
  The script copies `config/autoload/local.php.dist` to `config/autoload/local.php` if the latter does not exist yet.

```json
"post-update-cmd": [
    "php bin/composer-post-install-script.php"
],
"static-analysis": "phpstan analyse --memory-limit 1G"
```

#### Controllers replaced by handlers and the `routes` configuration

`dotkernel/dot-controller` is removed and request controllers are replaced by PSR-15 request handlers.

- [#33](https://github.com/dotkernel/light/pull/33) removes `dot-controller` and replaces the controllers with handlers.
  It also adds the `routes` key to `config/autoload/local.php.dist` and removes `403.html.twig`.
- [#43](https://github.com/dotkernel/light/pull/43) refactors the page handler to follow the naming standard.
  `Light\Page\Controller\PageController` is removed and `Light\Page\Handler\GetPageViewHandler` is added.
  The same pull request renames the `dot_log` writer keys from `priority` to `level`, raises `dot-errorhandler` to 4.2.1 and removes the `mezzio` Composer script.
- [#47](https://github.com/dotkernel/light/pull/47) renames the factories to `GetPageViewHandlerFactory` and `GetIndexViewHandlerFactory`.

The classes at tag `1.5.0` are:

- `Light\App\Handler\GetIndexViewHandler`, with `Light\App\Factory\GetIndexViewHandlerFactory`
- `Light\Page\Handler\GetPageViewHandler`, with `Light\Page\Factory\GetPageViewHandlerFactory`

Routing changed as well:

- The home page is served by `Light\App\RoutesDelegator` under the route name `app::index`, which replaces the route name `home`.
  The template is now `app::index` (`index.html.twig`), which replaces `app::home`.
- The `/page[/{action}]` route is removed.
- `Light\Page\RoutesDelegator` reads the `routes` key of the configuration and registers a `/<prefix>/<uri>` route for each entry, named `<prefix>::<template>`.

If your `config/autoload/local.php` was copied from the `1.0.0` `local.php.dist`, add the `routes` key, otherwise the About and Who We Are pages are not registered:

```php
'routes' => [
    'page' => [
        'about'      => 'about',
        'who-we-are' => 'who-we-are',
    ],
],
```

The `application.name` key is no longer in `local.php.dist`.

Update the `dot_log` writer configuration in `config/autoload/error-handling.global.php` to the new keys:

```php
'FileWriter' => [
    'name'    => 'stream',
    'level'   => Logger::ALERT,
    'options' => [
        'stream'  => __DIR__ . '/../../log/error-log-{Y}-{m}-{d}.log',
        'filters' => [
            'allMessages' => [
                'name'    => 'level',
                'options' => [
                    'operator' => '>=',
                    'level'    => Logger::EMERG,
                ],
            ],
        ],
    ],
],
```

#### Twig renderer package

[#22](https://github.com/dotkernel/light/pull/22) replaces `dotkernel/dot-twigrenderer` with `mezzio/mezzio-twigrenderer`.

- `config/autoload/templates.global.php` no longer declares `dependencies`, `debug`, the `DateExtension` or the `appName` global.
  It now sets `timezone` to `UTC` and `extensions` and `globals` to empty arrays.
- `config/config.php` no longer lists `\Dot\Twig\ConfigProvider` and `\Dot\FlashMessenger\ConfigProvider`.
- `config/twig-cs-fixer.php` no longer registers the Dot `DateExtension`.
- The `extra.laminas` and `extra.mezzio` component whitelists are removed from `composer.json`, and `laminas/laminas-component-installer` moved to the end of the `allow-plugins` list.

If your templates use Twig extensions or the flash messenger that came with `dot-twigrenderer`, require and register them yourself.

#### Error handler

- [#45](https://github.com/dotkernel/light/pull/45) adds the full `dot-errorhandler` configuration to `config/autoload/error-handling.global.php`: the cookie, header, request, server, session and trace providers, each with its commented-out processor options.
  The server and trace providers are enabled, the others are disabled.
- [#111](https://github.com/dotkernel/light/pull/111) raises `dotkernel/dot-errorhandler` from 4 to 5.
  This is a major version, so check the `dot-errorhandler` documentation for changes before upgrading.

#### Frontend build

The frontend build moved from webpack to Vite.

- [#50](https://github.com/dotkernel/light/pull/50) replaces webpack with Vite.
  `webpack.config.js` is removed, `vite.config.js` is added and the `package.json` scripts are now `build` and `watch`.
- [#114](https://github.com/dotkernel/light/pull/114) moves all npm packages to `devDependencies`, stops committing lock files and git-ignores the built `public/css/app.css` and `public/js/app.js`.
  It also removes `tsconfig.json` and the `browserconfig.xml` and `mstile-150x150.png` favicon files.
- [#116](https://github.com/dotkernel/light/pull/116) adds `engines.node` to `package.json`, so Node.js must be `^20.19.0 || >=22.12.0`.
- [#90](https://github.com/dotkernel/light/pull/90) raises `vite` to `^8.0.0`.
  It only matters if you build assets with the skeleton's `package.json`.

Because the built files are no longer committed, build them after checkout:

```shell
npm install
npm run build
```

### Optional updates

None of the following changes how the application runs.

#### Dev tooling

- [#17](https://github.com/dotkernel/light/pull/17): `laminas/laminas-coding-standard` to `^3.0`. Run `composer cs-check` to see new findings.
- [#102](https://github.com/dotkernel/light/pull/102): `vincentlanglet/twig-cs-fixer` to `^4.0.0`.
- [#63](https://github.com/dotkernel/light/pull/63): PHPStan configuration and docblock-only changes in both `ConfigProvider` classes.
- [#82](https://github.com/dotkernel/light/pull/82): `cross-env` to v10.
- [#86](https://github.com/dotkernel/light/pull/86): `pre-commit` to v2.
- [#91](https://github.com/dotkernel/light/pull/91): `vite-plugin-css-injected-by-js` to v5.
- [#96](https://github.com/dotkernel/light/pull/96): `vite-plugin-minify` to v3.
- [#95](https://github.com/dotkernel/light/pull/95): `vite-plugin-static-copy` to `^4.1.0`, plus README tool versions.

The following Renovate updates are for npm packages that are not in the `package.json` at tag `1.5.0`, so they have no net effect:

- [#80](https://github.com/dotkernel/light/pull/80): `@rollup/plugin-alias` to v6.
- [#81](https://github.com/dotkernel/light/pull/81): `babel-loader` to v10.
- [#83](https://github.com/dotkernel/light/pull/83): `jquery` to v4.
- [#84](https://github.com/dotkernel/light/pull/84): `npm` to v11.
- [#87](https://github.com/dotkernel/light/pull/87): `sass-loader` to v17.
- [#89](https://github.com/dotkernel/light/pull/89): `typescript` to v6.
- [#107](https://github.com/dotkernel/light/pull/107): `typescript` to v7.
- [#108](https://github.com/dotkernel/light/pull/108): `npm` to v12.

#### Templates and cosmetics

- [#24](https://github.com/dotkernel/light/pull/24): home page spacing and text tweaks.
- [#54](https://github.com/dotkernel/light/pull/54): new title and PSR-15 wording on the index page, new application name in `app.global.php`, and a Documentation link in the top menu.

#### Documentation and repository files

- [#19](https://github.com/dotkernel/light/pull/19): fixed the broken `LICENSE` link in `README.md`.
- [#26](https://github.com/dotkernel/light/pull/26): added the documentation link to `README.md`.
- [#38](https://github.com/dotkernel/light/pull/38): removed the "Configuration - First Run" section.
- [#55](https://github.com/dotkernel/light/pull/55): updated `.gitignore`.
- [#56](https://github.com/dotkernel/light/pull/56): removed `public/.DS_Store`.
- [#57](https://github.com/dotkernel/light/pull/57): removed `public/images/app/.DS_Store`.
- [#60](https://github.com/dotkernel/light/pull/60): README update about static modules.
- [#66](https://github.com/dotkernel/light/pull/66): README badge for the Packagist dependency version.

#### CI and automation

- [#5](https://github.com/dotkernel/light/pull/5), [#13](https://github.com/dotkernel/light/pull/13), [#34](https://github.com/dotkernel/light/pull/34), [#64](https://github.com/dotkernel/light/pull/64), [#71](https://github.com/dotkernel/light/pull/71), [#74](https://github.com/dotkernel/light/pull/74), [#94](https://github.com/dotkernel/light/pull/94), [#101](https://github.com/dotkernel/light/pull/101) and [#113](https://github.com/dotkernel/light/pull/113): Qodana workflow and action updates.
- [#40](https://github.com/dotkernel/light/pull/40): run PHPStan on PHP 8.4 as well.
- [#75](https://github.com/dotkernel/light/pull/75): added `renovate.json`.
- [#98](https://github.com/dotkernel/light/pull/98): added the `build-assets.yml` workflow that builds the JS and CSS assets.
- [#76](https://github.com/dotkernel/light/pull/76) and [#106](https://github.com/dotkernel/light/pull/106): `actions/cache` to v5 and v6.
- [#77](https://github.com/dotkernel/light/pull/77) and [#104](https://github.com/dotkernel/light/pull/104): `actions/checkout` to v6 and v7.
- [#79](https://github.com/dotkernel/light/pull/79) and [#99](https://github.com/dotkernel/light/pull/99): `codecov/codecov-action` to v6 and v7.
- [#109](https://github.com/dotkernel/light/pull/109): `actions/setup-node` to v7.

## FAQ

### Which PHP versions does 1.5 support?

PHP 8.3, 8.4 and 8.5.
PHP 8.2, supported by 1.0.0, was dropped together with the move to PHPUnit 12.

### Are there database migrations?

No.
The changes between 1.0.0 and 1.5.0 do not touch entities or migrations.

### Which configuration changed or moved?

- `config/autoload/local.php`: add the `routes` key and remove `application.name` if you copied the file from 1.0.0.
- `config/autoload/error-handling.global.php`: the `dot_log` writer keys `priority` are now `level`, and the `dot-errorhandler` provider configuration is added.
- `config/autoload/templates.global.php` and `config/config.php`: changed with the Twig renderer package swap.
- `config/twig-cs-fixer.php` and `phpcs.xml`: changed with the same swap.

### Do I need to apply the optional updates?

No.
Skipping them does not change how the application runs.

### How do I rebuild the frontend after the move to Vite?

Run `npm install` and then `npm run build` with a supported Node.js version.
Use `npm run watch` during development.
