# Creating pages

## Register the page route

Open `config/autoload/local.php` and locate the **routes** key.
Under the **page** key you will find an associative array with a couple of already existing routes.
You create a new route by appending a new line to that array:

```php
'example-page' => 'example-template',
```

> The array key is the page URI, the array value is the template name used by that page.

In order to be displayed this new `example-template` can then be added to the `src/Page/templates/page/example-template.html.twig` in the following way as an example:

```twig
    <li class="nav-item">
        <a class="nav-link" href="{{ url('page::example-template') }}">Example</a>
    </li>
```

## The page content

Each page has its own template, so the next step is to create the template files in the `src/Page/templates/page/` folder.
For the example above, the `src/Page/templates/page/example-template.html.twig` file was created.
We won't include the entire code here, just the basic building blocks.
The `content` block is where your page copy goes.

```twig
{% extends '@layout/default.html.twig' %}

{% block title %}Page Title{% endblock %}

{% block page_title %}{% endblock %}

{% block content %}
    <div class="page-intro">
        <div class="container">
            <h2>Add title here!</h2>
        </div>
    </div>

    <div>
        Add cool content here!
    </div>
{% endblock %}
```

### Grouping templates

The default grouping is under the `page` folder.
This item is defined in `src/Page/src/ConfigProvider.php` in `getTemplates()`, like seen below.

```php
    public function getTemplates(): array
    {
        return [
            'paths' => [
                'page' => [__DIR__ . '/../templates/page'],
            ],
        ];
    }
```

If you intend to group your templates into more folders, simply add another element under `paths`.

> It's not necessary to match the key name with the folder name.

```php
public function getTemplates(): array
{
    return [
        'paths' => [
            'page'    => [__DIR__ . '/../templates/page'],
            'how-tos' => [__DIR__ . '/../templates/how-tos'],
            'info'    => [__DIR__ . '/../templates/data'],
        ],
    ];
}
```

## Accessing the page

The url for the new page in this example is `/page/example-page`.

> Because of the way routing works, dot (.), dash (-), underscore (_) are filtered from the `action` parameter in the routing `/page[/{action}]`.
> As a result, the `examplePageAction` function in called.
