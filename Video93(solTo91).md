# `import.meta` in Node.js – Brief Revision Notes

## Definition
- `import.meta` is a special **metadata object** available only in **ECMAScript Modules (ESM)**.
- It provides information about the **current module**.

---

## When Can You Use It?
- ✅ In `.mjs` files.
- ✅ In `.js` files when `package.json` contains:

```json
{
  "type": "module"
}
```

- ❌ Not available in **CommonJS** modules.

---

## Main Property: `import.meta.url`

Returns the **file URL** of the current module.

```javascript
console.log(import.meta.url);
```

Example Output:

```text
file:///C:/Users/Himanshi/project/index.js
```

---

## Replacing `__filename`

```javascript
import { fileURLToPath } from "url";

const __filename = fileURLToPath(import.meta.url);
```

- Converts the module URL into a normal file path.

---

## Replacing `__dirname`

```javascript
import path from "path";
import { fileURLToPath } from "url";

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);
```

- Gives the directory path of the current module.

---

## CommonJS vs ES Modules

| CommonJS | ES Modules |
|-----------|------------|
| `__filename` | `fileURLToPath(import.meta.url)` |
| `__dirname` | `path.dirname(fileURLToPath(import.meta.url))` |
| `require()` | `import` |
| `module.exports` | `export` |

---

## Common Uses
- Get the current module's file path.
- Get the current directory path.
- Read files relative to the current module.
- Resolve module-related URLs.

---

## Important Points
- `import.meta` is **only available in ES Modules**.
- The most commonly used property is **`import.meta.url`**.
- It is mainly used to recreate `__filename` and `__dirname` in ESM.

---

## Quick Revision

- `import.meta` → Metadata object for the current ES module.
- `import.meta.url` → URL of the current module.
- `fileURLToPath(import.meta.url)` → Equivalent of `__filename`.
- `path.dirname(fileURLToPath(import.meta.url))` → Equivalent of `__dirname`.
- Works only in **ES Modules**, not in **CommonJS**.
