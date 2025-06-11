Node.js's original module system is [CommonJs](https://nodejs.org/docs/latest/api/modules.html) (which uses `require` and `module.exports`).

Since Node.js was created, the [ECMAScript module system](https://nodejs.org/docs/latest/api/esm.html) (which uses `import` and `export`) has become standard and Node.js has added support for it.

Node.js will treat `.cjs` files as CommonJS modules and `.mjs` files as ECMAScript modules. It will treat `.js` files as whatever the default module system for the project is (which is CommonJS unless _package.json_ says `"type": "module",`).

1. [[difference-between-require&import]]
2. 