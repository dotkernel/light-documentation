# Assets and the Vite build

## Summary

Where asset source files live, where Vite builds and copies them to, and how to bust the browser cache when they change.

## Details

Assets are the static files used by your content: images, fonts, JavaScript, and SCSS.
[Vite](https://vite.dev/) compiles and copies them from `src/App/assets` into the `public` folder, which is the only folder the web server serves.

> Prerequisite software: Node.js.
> `package.json` declares `"engines": { "node": "^20.19.0 || >=22.12.0" }`, so you need Node 20.19 or later on the 20.x line, or Node 22.12 or later.
> Earlier 20.x releases satisfy "Node 20" and still fail the install.

We use Vite:

- To avoid network bottlenecks that can occur when your application has a lot of separate scripts and style sheets.
- To concatenate and compress (uglify) `.css` and `.js` files.
- To preprocess `.scss` files into `.css`.
- To copy the `fonts` and `images` used in your project, from the `assets` folder to the `public` folder.

## Install the dependencies

First install the dependencies into the `node_modules` directory:

```shell
npm install
```

If everything ran ok, you should see a new root folder named `node_modules` where all the npm packages are installed.
If `npm install` fails, this could be caused by user permissions for npm.
Our recommendation is to install npm through `Node Version Manager`.

## Build the assets

The `fonts` folder is copied flat into `public/fonts/`, but the `images` folder is copied under an extra `app/` segment - `src/App/assets/images/icon/hand.svg` becomes `public/images/app/icon/hand.svg`, not `public/images/icon/hand.svg`.
See `vite.config.js` for the exact mapping.
The `js` and `scss` files are minimized.

The `build` command compiles the components, overwriting as needed:

```shell
npm run build
```

The `watch` command compiles the components, then monitors the source files, and triggers their recompilation when one of them is changed:

```shell
npm run watch
```

## Source and destination

The source of these files is the `src/App/assets/` folder.
The destinations are not symmetrical - the `js` and `scss` trees are bundled into a single file each, and `images` lands in a subfolder of `public/images`:

| Source                  | Destination          | What happens                                  |
|-------------------------|----------------------|-----------------------------------------------|
| `src/App/assets/scss`   | `public/css/app.css` | compiled from SCSS and minified into one file |
| `src/App/assets/js`     | `public/js/app.js`   | bundled and minified into one file            |
| `src/App/assets/fonts`  | `public/fonts/`      | copied as is                                  |
| `src/App/assets/images` | `public/images/app/` | copied as is                                  |

The `images/app/` destination is the one that catches people out: a file at `src/App/assets/images/logo.png` is served from `public/images/app/logo.png`, not `public/images/logo.png`.

Reference the built files in your templates with `asset()`:

```twig
<link href="{{ asset('css/app.css') }}" rel="stylesheet" />
<script src="{{ asset('js/app.js') }}"></script>
<img src="{{ asset('images/app/logo.png') }}" alt="Logo" />
<link rel="preload" href="{{ asset('fonts/Avenir-Light.ttf') }}" as="font" type="font/ttf" crossorigin />
```

The first two are used by default in `src/App/templates/layout/default.html.twig`.

> The source and destination folders are configured in the `vite.config.js` file.

## Do not edit the `public` folder by hand

Treat `public/css`, `public/js`, `public/fonts` and `public/images/app` as build output.
Edit the matching files under `src/App/assets` and rebuild, or your change will be overwritten the next time anyone runs the build.

The build overwrites the files it produces, but it does not currently clear these folders first.
A file you remove from `src/App/assets` therefore stays behind in `public` until you delete it yourself, and a renamed asset leaves its old copy in place.
If you need a clean result, delete the generated folders before rebuilding.

`public/` also holds files Vite never touches at all: `index.php` (the application's entry point), `.htaccess`, and `robots.txt.dist`.
Neither `npm run build` nor `npm run watch` creates, deletes, or modifies them.
Vite's output directory (`public/`) sits outside its project root (`src/`), so by default Vite refuses to empty or otherwise manage anything there beyond the specific files its own plugins write - the compiled `css/app.css` and `js/app.js`, and the `fonts`/`images` copies.
You can edit `.htaccess` or `robots.txt.dist` freely; a rebuild will never revert them.

## Browser caching of `js` and `css`

One thing of note is that browsers cache the `js` and `css` files.
When you push changes to one or both the files, you may notice that updating the site keeps the old version of the files.

A simple solution to force the browsers to download the newer version of the files is to add a version parameter in the url.
Whenever you commit changes to those files, make sure to increase the value of the `v` parameter.

```twig
<link href="{{ asset('css/app.css?v=3') }}" rel="stylesheet" />
...
<script src="{{ asset('js/app.js?v=5') }}"></script>
```

> The values 3 and 5 are provided as an example.
> The important thing is to use values for each file that you haven't used before, so incrementing the value for `v` is a simple way to track each change.

## FAQ

**Q: Where do image assets actually end up after the build?**
A: Under `public/images/app/`, not `public/images/` directly - the `images` copy target in `vite.config.js` adds an `app/` segment that `fonts` doesn't.

**Q: How do I force browsers to fetch an updated CSS or JS file?**
A: Add or increment a `?v=` query parameter on the asset URL, for example `app.css?v=3`.

**Q: Should I edit files directly under `public/css`, `public/js`, `public/fonts` or `public/images`?**
A: No - the `npm` script overwrites the files it produces, but it does not clear these folders first, so your manual edit may survive until the matching source file changes, then disappear unpredictably.
