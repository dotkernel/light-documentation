# Bundle Static Modules

## Summary

How to install and run the Vite build that compiles Dotkernel Light's front-end assets into the `public` folder.

## Details

> Prerequisite software: Node.js `^20.19.0 || >=22.12.0` (per `package.json`)

[Vite](https://vite.dev/) is a frontend dev tool we use:

- To avoid network bottlenecks that can occur when your application has a lot of separate scripts and style sheets.
- To concatenate and compress (uglify) `.css` and `.js` files
- To preprocess `.scss` files into `.css`.
- To copy the `fonts` and `images` used in your project, from the `assets` folder to the `public` folder.

First you need to install dependencies into the `node_modules` directory by running this command:

```shell
npm install
```

If everything ran ok, you should see a new root folder named `node_modules` where all the npm packages are installed.
If `npm install` fails, this could be caused by user permissions for npm.
Our recommendation is to install npm through `Node Version Manager`.

The `watch` command compiles the components then monitors the source files and triggers their recompilation when one of them is changed:

```shell
npm run watch
```

Initially, Vite is configured to delete and rebuild the contents of these folders from the `public` folder:

- css
- fonts
- images
- js

The folders are populated from their counterparts in `src/App/assets`, with one exception: images are copied into `public/images/app/`, not `public/images/` directly, so template references look like `{{ asset('images/app/logo.svg') }}`. `fonts` has no such prefix and is copied flat into `public/fonts/`. See `vite.config.js` for the exact mapping.

> Make sure to not edit anything inside the four public folders manually.
> Other files and folders in the public folder will be left as is.

An alternative to the `watch` command is `build` which simply compiles the components, overwriting as needed:

```shell
npm run build
```

## FAQ

**Q: What is the minimum Node.js version Dotkernel Light supports?**
A: `^20.19.0 || >=22.12.0`, as declared in `package.json`'s `engines` field.

**Q: What's the difference between `npm run watch` and `npm run build`?**
A: `watch` recompiles automatically whenever a source file changes; `build` compiles once.

**Q: Can I edit the compiled files under `public/css`, `public/js`, `public/fonts` or `public/images` directly?**
A: No — Vite deletes and rebuilds those four folders on every run, from their counterparts in `src/App/assets`.
