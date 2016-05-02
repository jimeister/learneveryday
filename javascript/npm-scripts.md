# npm scripts

`package.json` supports a scripts section which allows execution of arbitrary scripts via `npm run <script-name>`. For example:

```
{
  ...
  ...
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js",
    "compile": "node bin/compile"
  },
  ...
  ...
}
```

To start server, just run `npm run start`. To compile (i.e. run webpack compile), run `npm run compile`.

[reference](https://docs.npmjs.com/misc/scripts)
