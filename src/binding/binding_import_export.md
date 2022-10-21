# Import from/Export to JS

Rescript supports 2 JS import/export formats.
- Common JS: `require("MyFile")` and `module.exports = ...`
- ES6 modules: `import * from MyFile` and `export let ...`

It can be configured via `bsconfig.json`
```json
{
  "package-specs": {
    "module": "commonjs",
    "in-source": true
  }
}
```
```"module": "es6``` resolves `node_modules` using relative paths.

### Export to JavaScript
- named exporting is already there
- for default export, just `let default = 123`. 

A JavaScript default export is really just syntax sugar for a named export implicitly called `default`.

