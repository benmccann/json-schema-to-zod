# Json-Schema-to-Zod

[![NPM Version](https://img.shields.io/npm/v/json-schema-to-zod.svg)](https://npmjs.org/package/json-schema-to-zod)
[![NPM Downloads](https://img.shields.io/npm/dw/json-schema-to-zod.svg)](https://npmjs.org/package/json-schema-to-zod)

_Looking for the exact opposite? Check out [zod-to-json-schema](https://npmjs.org/package/zod-to-json-schema)_

## Summary

A runtime package and CLI tool to convert JSON schema (draft 4+) objects or files into Zod schemas in the form of JavaScript code. Uses Prettier for formatting, .

## Usage

### Online

[Just paste your JSON schemas here!](https://stefanterdell.github.io/json-schema-to-zod-react/)

### CLI

Installation:

> `npm i -G json-schema-to-zod`

Example:

> `json-schema-to-zod -s myJson.json -t mySchema.ts`

#### Options

| Flag                 | Shorthand | Function                                                |
| -------------------- | --------- | ------------------------------------------------------- |
| `--source`           | `-s`      | Source file name (required)                             |
| `--target`           | `-t`      | Target file name                                        |
| `--name`             | `-n`      | The name of the schema in the output                    |
| `--deref`            | `-d`      | Uses `json-schema-ref-parser` to dereference the schema |
| `--without-defaults` | `-wd`     | Ignore default values in the schema                     |

### Programmatic

`jsonSchemaToZod` will output the full module code, including a Zod import. If you only need the Zod schema itself, try one of the parsers directly. If you need to deref your JSON schema, try awaiting `jsonSchemaDereffed`.

```typescript
import {
  jsonSchemaToZod,
  jsonSchemaToZodDereffed,
  parseSchema,
} from "json-schema-to-zod";

const myObject = {
  type: "object",
  properties: {
    hello: {
      type: "string",
    },
  },
};

const module = jsonSchemaToZod(myObject);

const dereffed = await jsonSchemaToZodDereffed(myObject);

const schema = parseSchema(myObject);
```

`module`/`dereffed` =

```typescript
import { z } from "zod";

export default z.object({ hello: z.string().optional() });
```

`schema` =

```typescript
z.object({ hello: z.string().optional() });
```
