# Bundle Static Modules

Vite is a frontend dev tool we use:

- To avoid network bottlenecks that can occur when your application has a lot of separate scripts and style sheets.
- To concatenate and compress (uglify) `.css` and `.js` files
- To preprocess `.scss` files into `.css`.
- To copy the `fonts` and `images` used in your project, from the `assets` folder to the `public` folder.

First you need to install dependencies into the `node_modules` directory by running this command:

```shell
npm install
```

If `npm install` fails, this could be caused by user permissions of npm.
Recommendation is to install npm through `Node Version Manager`.

The build command compiles the components then monitors the source files and triggers their recompilation when one of them is changed:

```shell
npm run build
```  

To review the project via Vite, you can use this command that starts the PHP server on port 8080:

```shell
npm run preview
```

The above command executes `php -S 0.0.0.0:8080 -t public`, with the added benefit that it refreshes the page whenever a recompilation is completed.
