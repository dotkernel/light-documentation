# Edit the top menu

The top menu is displayed on all the pages, in the header.
To edit it, go to `src/App/templates/layout/default.html.twig` and update the items under `id="navbarHeader"`.

You can use the below as an example.

```twig
<div class="menu" id="navbarHeader">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="pageDropdown" data-bs-toggle="dropdown" aria-haspopup="true" aria-expanded="false">Grouped Pages</a>
        <div class="dropdown-menu" aria-labelledby="pageDropdown">
          <a class="dropdown-item" href="{{ url('page', {action: 'home'}) }}">Home</a>
          <a class="dropdown-item" href="https://www.example.com/docs">Docs</a>
        </div>
      </li>
      <li class="nav-item">
          <a class="nav-link" target="_blank" href="{{ url('page', {action: 'firstLink'}) }}">First Link</a>
      </li>
      <li class="nav-item">
          <a class="nav-link" target="_blank" href="https://second.example.com/">Second Link</a>
      </li>
    </ul>
</div>
```

Each `li` element is listed as an item in the top menu.

There are two different types of elements in the example:

- The `Grouped Pages` group several urls.
When you click on the item, the elements grouped under it are listed and can be accessed.
They can be internal and/or external links.
- The `First Link` and `Second Link` are regular links, one an internal link and the other an external one.

> You can also replace the `nav-item` class for the `li` elements with `button-border` for a link that looks more like a button.
