# Twitter and OpenGraph cards

If you want to promote your pages on other platforms, you can post Twitter (X) and OpenGraph cards in the header section in the `src/App/templates/layout/default.html.twig` file.

Make sure to update all items based on your page content.

```twig
<!-- Twitter card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@example">
<meta name="twitter:title" content="Page title">
<meta name="twitter:description" content="Basic description">
<meta name="twitter:image" content="{{ url('home') }}images/app/My-image.png">
<meta name="twitter:image:alt" content="Image alt">

<!-- OpenGraph card -->
<meta property="og:title" content="Page title"/>
<meta property="og:type" content="website"/>
<meta property="og:url" content="{{ url('home') }}"/>
<meta property="og:image" content="{{ url('home') }}images/app/My-image.png"/>
<meta property="og:description" content="Basic description"/>
```

In the example:

- {{ url('home') }} is the URL for the homepage, but you can also use this code to generate the url for other pages, just like in the canonical URL `{% block canonical %}{{ url(routeName ?? null) }}{% endblock %}`.
  - The `block` item is present to mitigate for not-found pages, e.g. when the url is typed incorrectly.
- The image from `{{ url('home') }}images/app/My-image.png` is found in `public/images/app/PHP-REST-API.png`, but it is copied there by the `npm` script from `src/App/assets/images/PHP-REST-API.png`.
