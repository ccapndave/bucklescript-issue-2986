# react

## Run Project

```sh
npm install
npm start
```

Suppose you have a http-server running (try `npm i -g http-server`)


Then modify whichever `.re` file in `src` and refresh the page to see the changes.

**For more elaborate ReasonReact examples**, please see https://github.com/reasonml-community/reason-react-example

# bucklescript-issue-2986

This repository was created with these steps:

1. `bsb -init bucklescript-issue-2986 -theme react-lite`
2. `yarn add bs-css`
3. Add `bs-css` to `bsconfig.json` dependencies
4. Replaced all reason code with the simplest call that invokes `bs-css`, which is `Css.style([])`;

If you then compile and open the page in the browser you will see the following error:

```
loader.js:346 Uncaught (in promise) Error: glamor@http://localhost:8080/node_modules/bs-css/src/Css.js was not resolved successfully
```

This is caused by an incorrect path for one of `Css.js`'s dependencyies; specifically

http://localhost:8080/node_modules/glamor.js

instead of

http://localhost:8080/node_modules/lib/glamor.js

The root cause of this seems to be that the `main` field in `glamor`'s `package.json` isn't being respected.
