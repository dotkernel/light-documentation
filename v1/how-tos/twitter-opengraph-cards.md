# Twitter and OpenGraph cards

If you want to promote your pages on other platforms, you can post Twitter (X) and OpenGraph cards in the header section in the `src/App/templates/layout/default.html.twig` file.

Make sure to update all items based on your page content.

```twig
<!-- Twitter card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@example">
<meta name="twitter:title" content="Page title">
<meta name="twitter:description" content="Basic description">
<meta name="twitter:image" content="{{ absolute_url(asset('images/app/My-image.png')) }}">
<meta name="twitter:image:alt" content="Image alt">

<!-- OpenGraph card -->
<meta property="og:title" content="Page title"/>
<meta property="og:type" content="website"/>
<meta property="og:url" content="{{ url('app::index') }}"/>
<meta property="og:image" content="{{ absolute_url(asset('images/app/My-image.png')) }}"/>
<meta property="og:description" content="Basic description"/>
```

In the example:

- `{{ url('app::index') }}` is the absolute URL of the homepage, and `url()` returns an absolute URL for any route name, which is what cards require — you can point a card at another page the same way, just like the canonical URL does in `{% block canonical %}{{ url(routeName ?? null) }}{% endblock %}`.
    - The `block` item is present to mitigate for not-found pages, e.g. when the url is typed incorrectly.
- Card images must be absolute URLs too, but `asset()` on its own returns a path, so it is wrapped in `absolute_url()`.
The image from `{{ absolute_url(asset('images/app/My-image.png')) }}` is found in `public/images/app/PHP-REST-API.png`, but it is copied there by the `npm` script from `src/App/assets/images/PHP-REST-API.png`.
