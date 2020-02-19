# ie11 corejs stack overflow

When
[get-own-property-symbols](https://github.com/es-shims/get-own-property-symbols)
is included before [core-js
web.dom-collections.iterator](https://github.com/zloirock/core-js/blob/master/packages/core-js/modules/web.dom-collections.iterator.js),
it causes ie11 to stack overflow.

This repo is a minimal reproduction of this error. To test, run:

```bash
npm install
npm run build
```

And then open `./dist/index.html` in ie11.

## More background

get-own-property-symbols is included within the
[webcomponentsjs](https://github.com/webcomponents/polyfills/tree/master/packages/webcomponentsjs)
polyfills for custom elements. To properly use it in an app, it needs to
be a script included in the `head` of the document.

If that app also uses core-js, which it would if it is using
`@babel/preset-env` with [useBuiltIns:
'usage'](https://babeljs.io/docs/en/babel-preset-env#usebuiltins-usage),
then it will cause a stack overflow in ie11.

## Screenshot of debugger during infinite recursion

![screenshot of ie11 debugger](/ie11-debugger.png)
