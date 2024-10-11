# Manage Assets

If you haven't already done so, make sure `npm` is installed.
You can keep it running during your updates with `npm run watch` or run this command after the edits are completed `npm run prod`.

## What are assets?

Assets are various files used by your content:

- Images,
- Fonts,
- JavaScript codes,
- SCSS.

## Assets source and destination

The source of these files is the `src/App/assets/` folder:

- src/App/assets/images
- src/App/assets/fonts
- src/App/assets/js
- src/App/assets/scss

The `npm` script processes these files and copies or builds files under the `public` folder.

> You should not manage the items from the above folders manually.
> The `npm` script will delete/replace the files when run.

While the `images` and `fonts` folders are copied as is, the `js` and `scss` are minimized:

- `scss` files are minimized under `public/js/app.css`.
- `js` files are minimized under `public/js/app.js`.

The above items are by default used in the `src/App/templates/layout/default.html.twig` file.

```twig
<link href="{{ asset('css/app.css') }}" rel="stylesheet" />
...
<script src="{{ asset('js/app.js') }}"></script>
```

> The source and destination folders are configured in the `webpack.config.js` file.

## Browser caching of `js` and `css`

One thing of note is that browsers cache the `js` and `css` files.
When you push changes to one or both the files, you may notice that updating the site keeps the old version of the files.

A simple solution to force the browsers to download the newer version of the files is to add a version parameter in the url.
Whenever you commit changes to those files, make sure to increase the value of the `v` parameter.

```twig
<link href="{{ asset('css/cls_dk.css?v=3') }}" rel="stylesheet" />
...
<script src="{{ asset('js/cls_dk.js?v=5') }}"></script>
```
> The values 3 and 5 are provided as an example.
> The important thing is to use values for each file that you haven't used before, so incrementing the value for `v` is a simple way to track each change.
