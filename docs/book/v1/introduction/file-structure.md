# File structure

Dotkernel Light follows the [PSR-4](https://www.php-fig.org/psr/psr-4/) standards.

It is a good practice to standardize the file structure of projects.

When using Dotkernel Light, the following structure is installed by default:

![Dotkernel Light File Structure!](https://docs.dotkernel.org/img/light/file-structure-dk-light.png)

## Special purpose folders

* `.github` - contains the GitHub Actions workflow files

## Root files

These files sit at the root of the repository:

* `.gitattributes` - normalises line endings, and marks which files Git treats as binary or diffs as markdown
* `CHANGELOG.md` - the release history
* `LICENSE` - the project licence
* `OSSMETADATA` - declares the open source lifecycle state of the project
* `README.md` - the project readme
* `SECURITY.md` - the supported versions and the process for reporting a vulnerability
* `composer.json` - PHP dependencies, autoloading, and the `composer` scripts listed throughout this documentation
* `package.json` - front-end dependencies, and the `npm run build` and `npm run watch` scripts
* `phpcs.xml` - PHP_CodeSniffer configuration, used by `composer cs-check` and `composer cs-fix`
* `phpstan.neon` - PHPStan configuration, used by `composer static-analysis`
* `phpunit.xml` - PHPUnit configuration, used by `composer test`
* `renovate.json` - Renovate configuration for automated dependency updates
* `vite.config.js` - the Vite build configuration; see [Manage Assets](../how-tos/manage-assets.md)

## `bin` folder

This folder contents are

* `clear-config-cache.php` - Removes the config cache file `data/cache/config-cache.php`; also available as `composer clear-config-cache`
* `composer-post-install-script.php` - Runs automatically on Composer's `post-update-cmd` hook, and copies the distributed local configuration template in `config/autoload/` into place unless that file already exists

## `config` folder

This folder contains all application-related config files:

* `config.php` - Registers ConfigProviders for installing packages
* `container.php` - Main service container that provides access to all registered services
* `development.config.php.dist` - Activates debug mode; gets symlinked as `development.config.php` when enabling development mode
* `pipeline.php` - Contains a list of middlewares, in the order of their execution
* `twig-cs-fixer.php` - Configuration file for Twig code style checker/fixer

### `config/autoload` folder

This folder contains all service-related local and global config files:

* `app.global.php` - Configures basic app variables
* `dependencies.global.php` - Config file to set global dependencies that should be accessible by all modules
* `development.local.php.dist` - Gets symlinked as `development.local.php` when enabling development mode; activates error handlers
* `error-handling.global.php` - Configures and activates error logs
* `local.php.dist` - Local config file where you can overwrite application name and URL
* `mezzio.global.php` - Mezzio core config file
* `templates.global.php` - mezzio/mezzio-twigrenderer config file

## `data/cache` folder

This folder is a storage for service caches.

## `log` folder

This folder stores daily log files.
When you access the application from the browser, (if not already created) a new log file gets created in the format specified in the `config/autoload/error-handling.global.php` config file under the `stream` array key.

## `public` folder

This folder contains all publicly available assets and serves as the entry point of the application:

* `css` and `js` - Contain the css and js file(s) built by Vite from the assets folder
* `fonts` and `images` - Contain the font and image file(s) copied by Vite from the assets folder
* `.htaccess` - server configuration file used by Apache web server; it enables the URL rewrite functionality
* `index.php` - the application's main entry point
* `robots.txt.dist` - a sample robots.txt file that allows/denies bot access to certain areas of your application; activate it by duplicating the file as `robots.txt` and comment out the lines that don't match your environment

## `src` directory

This folder contains a separate folder for each Module.

These are the modules included by default:

* `App` - Core functionality, from rendering, to error reporting
* `Page` - Contains functionality for displaying a page

`src/App/assets` holds the front-end sources — `js`, `scss`, `fonts` and `images` — that Vite compiles and copies into the `public` folder.

### Module contents

Each Module folder, in turn, should contain the following folders, unless they are empty:

* `src/Factory` - Factories which provide handler/service dependencies
* `src/Handler` - Request handlers
* `src/Service` - Service classes

The `src` folder in each Module folder normally also contains these files:

* `ConfigProvider.php` - Configuration data for the module
* `RoutesDelegator.php` - Module specific route registrations

### `templates` directory for modules

This directory contains the template files.

> `Twig` is used as templating engine.
> All template files have the extension `.html.twig`.

## `test` folder

This folder contains the application's test suite.
`test/Unit` holds the unit tests, which run with `composer test`.
