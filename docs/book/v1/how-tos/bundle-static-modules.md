# Bundle Static Modules

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

The build command compiles the components then monitors the source files and triggers their recompilation when one of them is changed:

```shell
npm run build
```  

Initially, Vite is configured to delete and rebuild the contents of these folders from the `public` folder':

- css
- fonts
- images
- js

The folders are populated from their counterparts in `src/App/assets`.

> Make sure to not edit anything inside the four public folders manually.
> Other folders and the three initial files in the public folder will be left as is.

To review the project via Vite, you can use this command that starts the PHP server on port 8080:

```shell
npm run preview
```

The above command executes `php -S 0.0.0.0:8080 -t public`, with the added benefit that it refreshes the page whenever a recompilation is completed.
