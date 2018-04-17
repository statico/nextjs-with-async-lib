# nextjs with async library demo

## Problem

I need a library to be accessible from Node on the server-side and from NextJS React pages.

I would like to take advantage of the new async/await syntax because it makes the code remarkably cleaner and easier to debug.

## Bug

This demo shows weirdness when trying to include a JavaScript library with async functions inside of a NextJS page:

```
$ yarn install
$ yarn exec next
 WARNING  Compiled with 2 warnings

 warning  in ./pages/index.js

24:18-21 "export 'foo' was not found in '../lib/test'

 warning  in ./pages/index.js

24:62-65 "export 'foo' was not found in '../lib/test'

TypeError: Cannot assign to read only property 'exports' of object '#<Object>'
...
```

And visiting http://localhost:3000 --

![](https://i.imgur.com/n1aSUY2.png)

I can't change `lib/test.js` to ES6-style `export`s because Node will complain with `SyntaxError: Unexpected token`. What am I doing wrong?

### Versions

- NextJS 5.1
- Node 9.11.1

### Related issues

- https://github.com/webpack/webpack/issues/4039
- https://github.com/zeit/next.js/issues/3650

### pages/index.js

```javascript
import { foo } from '../lib/test'

export default () => <div>hello {String(typeof foo)}</div>
```

### lib/test.js

```javascript
async function foo () {}

module.exports = { foo }
```
