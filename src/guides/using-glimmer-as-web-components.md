# Using Glimmer as Web Components

In addition to using Glimmer for a widget on one section on a page, you can also use Glimmer components as web components.

## Generating a new app

Let's do another new app setup. Instead of doing an installation like we did originally, we'll now run the following command:

```sh
ember new display-tile -b @glimmer/blueprint --web-component
```

When we add the `--web-component` flag, we reconfigure our app to expose our `display-tile` component as a Web Component to browsers. That in turn allows us to render markup like the following from a backend:

```hbs
<display-tile></display-title>
```

Once we add our `app.js` file to the page, our browser will automatically load our Glimmer component into the DOM using the options provided by the backend and will boot each Glimmer app.

## Adding to an existing app

If you already have an app and you want to use it as a Web Component, install the following package using yarn:

```sh
$ yarn add --dev @glimmer/web-component
```

or npm:

```sh
npm install --save-dev @glimmer/web-component
```

After the package is installed, you will have to add two lines to `src/index.ts`. First, the following import:

```ts
import initializeCustomElements from '@glimmer/web-component';
```

Then, after `app.boot()`, the following line of code:

```ts
initializeCustomElements(app, [/* component names */]);
```

This will register custom elements for each of the component names you give to `initializeCustomElements` and will replace the custom element with your Glimmer component once the custom element connects.
For example, if you provide the component name `'foo-bar'` you can now use the custom element `<foo-bar>` anywhere in the DOM and have your `foo-bar` component render in its place.

## More

For more information about web components, browser support and various polyfills to enable broader support, please see:

- [https://www.webcomponents.org/introduction](https://www.webcomponents.org/introduction)
- [https://www.webcomponents.org/polyfills](https://www.webcomponents.org/polyfills)
- [http://jonrimmer.github.io/are-we-componentized-yet/](http://jonrimmer.github.io/are-we-componentized-yet/)

*Note* You cannot currently pass arguments to top-level Glimmer components due to technical limitations. We are working on removing this restriction.
