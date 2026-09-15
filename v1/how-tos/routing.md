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
To clarify, this creates a route called `page::about` in the `page` module, it loads the template file `src/Page/templates/page/about.html.twig` and can be accessed at `/page/about`.
The separator between the prefix and the template name is a double colon, so `url('page::about')` resolves, while `url('page.about')` throws.
With each request, when matching one of these routes, the `GetPageViewHandler` will detect the current route name and render the matching template.

### Manipulating the declared routes and modules

Each module registers its routes in a `RoutesDelegator.php` file, and the two modules do this differently.
`src/Page/src/RoutesDelegator.php` retrieves the application config from the container and loops over each prefix and its assigned routes:

```php
    $routes = $container->get('config')['routes'] ?? [];
    foreach ($routes as $prefix => $moduleRoutes) {
        foreach ($moduleRoutes as $routeUri => $templateName) {
            $app->get(
                sprintf('/%s/%s', $prefix, $routeUri),
                GetPageViewHandler::class,
                sprintf('%s::%s', $prefix, $templateName)
            );
        }
    }
```

`src/App/src/RoutesDelegator.php` declares no config-driven routes at all — it registers a single static route for the home page:

```php
    $app->get('/', [GetIndexViewHandler::class], 'app::index');
```
