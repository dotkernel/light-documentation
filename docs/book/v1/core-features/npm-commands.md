# NPM Commands

To install dependencies into the `node_modules` directory run this command.

```shell
npm install
```

If `npm install` fails, this could be caused by user permissions of npm.
Recommendation is to install npm through `Node Version Manager`.

The watch command compiles the components then watches the files and recompiles when one of them changes:

```shell
npm run watch
```  

When you are done making changes to your code, this command compiles the assets locally, minifies them and makes them ready for production:

```shell
npm run prod
```
