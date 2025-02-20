# Routing

In our current implementation we are using request handlers instead of controllers in order for DotKernel to comply with the PSR-15 standard.

## How are we implementing handlers?

### Declaration of the routes and modules

Currently, our structure uses modules, routes and template names.
Those are being declared in the file `config/autoload/local.php` in the following way:

```php
    'routes'      => [
        'page' => [
            'about'      => 'about',
            'who-we-are' => 'who-we-are',
        ],
    ],
```

In this case `page` represents the module and `'about' => 'about'` represents the page slug and its assigned `.twig` template.
To clarify, this creates a route called `page.about` in the `page` module, it loads the template file `src/Page/templates/page/about.html.twig` and can be accessed at `/page/about`.
With each request, when matching one of these routes, the `PageHandler` will detect the current route name and render the matching template.

### Manipulating the declared routes and modules

Each module has a `RoutesDelegator.php` file (ex. `src/Page/src/RoutesDelegator.php`).
In this file we are retrieving the application config from the container and we loop over each module and their assigned routes.

```php
    $routes = $container->get('config')['routes'] ?? [];
    foreach ($routes as $moduleName => $moduleRoutes) {
        foreach ($moduleRoutes as $routeUri => $templateName) {
            $app->get(
                sprintf('/%s/%s', $moduleName, $routeUri),
                [PageHandler::class],
                sprintf('%s::%s', $moduleName, $templateName)
            );
        }
    }
```
