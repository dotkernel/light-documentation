# File structure

Dotkernel Light follows the [PSR-4](https://www.php-fig.org/psr/psr-4/) standards.

It is a good practice to standardize the file structure of projects.

When using DotKernel Light, the following structure is installed by default:

![Dotkernel Light File Structure!](https://docs.dotkernel.org/img/light/file-structure-dk-light.png)

## Main directories

* `bin` - various helper scripts
* `config` - various configuration files
* `data` - should contain project-related data
* `log` - storage of log files generated by dot-error-log library
* `public` - publicly visible files. The webserver need to have this folder as www-document root folder.
* `src` - should contain the source code files
* `test` - should contain the test files

### `bin` directory

This directory contains one file, `clear-config-cache.php` which removes the config cache file (`data/cache/config-cache.php` - available only when development mode is enabled).

### `config` directory

This directory contains all application-related config files:

* `config.php`: here you will register ConfigProviders after installing packages
* `container.php`: main service container, providing access to all registered services
* `development.config.php.dist`: gets symlinked as `development.config.php` when enabling development mode - activates debug mode
* `pipeline.php`: contains a list of middlewares, in their order of execution
* `twig-cs-fixer.php`: configuration file for Twig code style checker/fixer

#### `autoload` directory

This directory contains all service-related local and global config files:

* `app.global.php`: sets the application name
* `dependencies.global.php`: config file to set global dependencies that should be accessible by all modules
* `development.local.php.dist`: gets symlinked as `development.local.php` when enabling development mode - activates error handlers
* `error-handling.global.php`: configures and activates error logs
* `local.php.dist`: local config file where you can overwrite application name and URL
* `mezzio.global.php`: Mezzio core config file
* `templates.global.php`: dotkernel/dot-twigrenderer config file

### `data` directory

This directory is a storage for project data files and service caches.
Inside you will find:

* `cache`: Twig's cache directory

> AVOID storing sensitive data on VCS.

### `log` directory

This directory stores daily log files.
When you access the application from the browser, (if not already created) a new log file gets created in the format specified in the `config/autoload/error-handling.global.php` config file under the `stream` array key.

### `public` directory

This directory contains all publicly available assets and serves as the entry point of the application:

* `css`: contains `app.css`, a single file containing the entire CSS code collected from all modules, in a minified form
* `fonts`: contains `app`, a directory containing custom font files collected from all modules
* `images`: contains `app`, a directory containing all image files collected from all modules
* `js`: contains `app.js`, a single file containing the entire JavaScript code collected from all modules, in a minified form
* `.htacess`: server configuration file used by Apache web server - this file enables the URL rewrite functionality
* `index.php`: the application's main entry point
* `robots.txt.dist`: a sample robots.txt file, providing settings allow/deny bot access to certain areas of your application - activate it by duplicating the file as `robots.txt` and comment out the lines that don't match your environment

### `src` directory

This directory contains two directories, called modules:

* `App`
* `Page`

#### `App` directory

This is the `App` module.
It contains all generic functionalities your application depends on.

The `assets` directory contains all generic assets, reusable across the application.

The `src` contains `ConfigProvider.php`, a file that sets template path aliases (`getTemplates`) but can also provide dependencies (`getDependencies`).

The `templates`: contains misc components like the home page, custom error pages, template partials and the default layout template.

#### `Page` directory

This is the `Page` module.
It contains page-related components for your application.

The `src` directory contains the following items:

* `Controller`: contains module controllers
* `Factory`: contains module factories, which are used to provide ready-to-use instances of certain classes
* `Service`: contains module service files, which contain classes that provide custom functionalities
* `ConfigProvider.php` - provides module configuration data
* `RoutesDelegator.php` - stored main routes found in the module

The `templates` directory contains the `page` directory, with template files for various web pages.

## Special purpose directories

* `.github`  - contains workflow files
* `.laminas-ci` - contains Laminas Continuous Integration (CI) workflow files
