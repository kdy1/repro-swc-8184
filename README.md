# swc-1.3.79-bug

I am using an Apple M1 chip, macOS Sonoma 14.0 system, and Node version 18.

1. Use @swc/core version 1.3.78, install dependencies, and run `npx swc src/ -d dist-1.3.78`.
2. Modify package.json to use @swc/core version 1.3.79, and run `npx swc src/ -d dist-1.3.79`.
3. Comparing the build results of dist-1.3.78 and dist-1.3.79, the first line in the index.js file of version 1.3.79 is import a from "./a/index.jsx", but in reality, there is no index.jsx file.

## .swcrc
```
{
  "jsc": {
    "parser": {
      "syntax": "typescript",
      "tsx": true
    },
    "baseUrl": "./",
    "paths": {
      "~/*": [
        "./src/*"
      ]
    }
  }
}
```

## dist-1.3.78/index.js
```
import a from "./a";
import b from "./b";
import c from "./c";
import d from "./d";
console.log(a, b, c, d);
```

## dist-1.3.79/index.js
```
import a from "./a/index.jsx";
import b from "./b/index.js";
import c from "./c";
import d from "./d";
console.log(a, b, c, d);
```
