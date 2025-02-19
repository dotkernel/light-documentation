# Routing

In our current implementation we are using request handlers instead of controllers in order for Dot Kernel to comply with the PSR-15 standard.

## How are we implementing handlers?

#### Declaration of the routes and modules:

Currently, our structure uses modules, routes and template names. Those are being declared in the file `config/autoload/local.php` in the following way:

```php
    'routes'      => [
        'page' => [
            'about'      => 'about',
            'who-we-are' => 'who-we-are',
        ],
    ],
```

In this case `page` represents the module and `'about' => 'about'` represents the route and its assigned `.twig` template.

#### Manipulating the declared routes and modules:

Each module has a `RoutesDelegator.php` file (ex. `src/Page/src/RoutesDelegator.php`). In this file we are retrieving the settings of the container
and we loop over each module and their assigned routes. Those routes are being passed to the app with a `PageHandler` for the purpose of rendering 
the template. 

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


