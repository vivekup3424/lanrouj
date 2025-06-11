Let me explain the key differences between `import` and `require`:

1. Syntax:
```javascript
// require (CommonJS)
const module = require('module-name');

// import (ES Modules)
import module from 'module-name';
```

2. Main Differences:
- `require` is synchronous and loads modules at runtime
- `import` is asynchronous and loads modules at parse time
- `require` can be called anywhere in the code
- `import` must be at the top level (outside any functions/conditions)

3. Flexibility:
```javascript
// require allows dynamic paths
const moduleName = 'myModule';
const module = require('./' + moduleName);

// import is static (though dynamic import() exists)
import module from './myModule';  // Must be static string
```

4. Module Systems:
- `require`: CommonJS (traditional Node.js)
- `import`: ECMAScript Modules (ESM, modern JavaScript)

5. Common Import Variations:
```javascript
// Named imports
import { function1, function2 } from 'module';

// Default import
import defaultExport from 'module';

// Import all as namespace
import * as moduleNamespace from 'module';

// Import for side effects only
import 'module';
```

6. Common Require Variations:
```javascript
// Destructuring require
const { function1, function2 } = require('module');

// Single exports
const specificFunction = require('module').function1;
```

The modern trend is toward using `import` as it's the official ECMAScript standard and offers better static analysis and [[Tree-shaking opportunities]]. However, `require` is still widely used, especially in Node.js environments.

Would you like me to elaborate on any of these aspects?
