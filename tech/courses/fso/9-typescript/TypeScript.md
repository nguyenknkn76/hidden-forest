# TypeScript
## Background and Introduction
TypeScript: is designed for large scale dev created by Microsoft.
Example: VS Code, Microsoft's Azure Management Portal 

### Main principle
TS being a superset of JS means all the features of JS and its addientional features as well.
TS consists of 3 parts:
- the language: syntax, keywords, type annotations → dev have the most contact with this one.
- compiler: removing the typing info and for code transformations (enable TS transpiled into executable JS) → (everything related to the types is removed at compile time)
  - compiling: code is transformed form a human readalbe format to a machine readable format.
  - transpling: in TS, human readable code is transformed into another human readable one.
- laguage service: collects type info. Dev tools can use the type infor for poviding intelisense, type hints and possible refactoring alternatives

### Key features
#### Type annotations
light weight way to record the intended contract of function or var
```ts
const birthdayGreeter = (name: string, age: number): string => {
  return `Happy birthday ${name}, you r now ${age} years old!`;
};
// in this case function birhtdayGreeter accepted 2 arguments one is string, one is number, and the function return a string
const birthdayHero = "Nguyen`;
const age = 23;

console.log(birthdayGreeter(birthdayHero, age));
```

#### Keywords
- somme words that be use in the construct the language.
- cannot be used as identifiers (var name, function name, class name)
- 40-50 keywords like: type, emum, interface, void, null, instaceof, ... etc

#### Structural typing
- structural typing
- nominal typing

#### Inference
```ts
const add = (a: number, b: number) => {
  /* The return value is used to determine
     the return type of the function */
  return a + b;
}
```
#### Type erasure
TS removes all type system contructs during compilation
in: `let x: SomeType;`
out:`let x;`

#### Why sould one use TS?
- Type checking and static code analysis
- Type annotations in the code can functino as a kind of code level doc.
- IDEs can provide more specific and smarter IntelliSense when they know exactly what types of data you r processing

#### What does TS cannot fix?
Some issues many have with TS:
- Incomplete, invalid or missing types in external lib
- Sometimes, type inference need assitance
  - [type assertions ](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions)
  - [type guarding/narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
- Mysterious type errors

## First step with TS
### Setting things up
- install ts-node and typescript: 
  - global: `npm install --location=global ts-node typescript`
  - project:`npm install --save-dev ts-node typescript`
- run file.ts with `ts-node` and option -s and --someoption, whole command is: `npm run ts-node file.ts -- -s --someoption`
```json
"scripts": {
  "ts-node": "ts-node"
},
```
**coding style** 
`tsconfig.json`: used to define how the TS compiler should interpret the code, how strictly the compiler should work, which file to watch and ignore,...etc
```json
{
  "compilerOptions":{
    "noImplicitAny": false
  }
}
```
> note: read more about tsconfig doc [here](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html).

### Creating ur first own types && Type narrowing
```ts
type Operation = 'multiply' | 'add' | 'divide';
type Result  = string || number;
/* 
  this is union types (read more here: https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)
*/
```
full version: 
```ts
type Operation = 'multiply' | 'add' | 'divide';
type Result  = string || number; // in case result u wanna return has 2 types number and string
const calculator = (a: number, b: number, op: Operation) : number => {
  switch(op) {
    case 'multiply':
      return a * b;
    case 'divide':

      if (b === 0) throw new Error('Can\'t divide by 0!');
      return a / b;
    case 'add':
      return a + b;
    default:

      throw new Error('Operation is not multiply, add or divide!');
  }
}

/* 
  this is using type narrowing
  - can't use error.message when error type is unknown
  → after using (error instanceof Error): the type is narrowed and we can refer to error.message
*/

try {
  console.log(calculator(1, 5 , 'divide'));
} catch (error: unknown) {
  let errorMessage = 'Something went wrong: '
  if (error instanceof Error) {
    errorMessage += error.message;
  }
  console.log(errorMessage);
}
```

>   read more about: 
> - [narrow ](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
> - [unknown](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type)
> - [Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error) 
> - [error message](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error/message)

### Accessing command line arguments
```ts
console.log(process.arvg)
```

### @types/{npm_package}
- install package with `@types/` prefix: `npm install --save-dev @types/react @types/express @types/lodash @types/jest @types/mongoose`

> read more about:
> - [peer dependencies](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#peerdependencies)

### Improve project
```ts
interface MultiplyValues {
  value1: number;
  value2: number;
}

// ensure that parameters gibven to func are of the right type.
const parseArguments = (args: string[]): MultiplyValues => {
  if (args.length < 4) throw new Error('Not enough arguments');
  if (args.length > 4) throw new Error('Too many arguments');

  if (!isNaN(Number(args[2])) && !isNaN(Number(args[3]))) {
    return {
      value1: Number(args[2]),
      value2: Number(args[3])
    }
  } else {
    throw new Error('Provided values were not numbers!');
  }
}

const multiplicator = (a: number, b: number, printText: string) => {
  console.log(printText,  a * b);
}

try {
  //  get the multiplier to work with command-line parameters 
  const { value1, value2 } = parseArguments(process.argv);
  multiplicator(value1, value2, `Multiplied ${value1} and ${value2}, the result is:`);
} catch (error: unknown) {
  let errorMessage = 'Something bad happened.'
  if (error instanceof Error) {
    errorMessage += ' Error: ' + error.message;
  }
  console.log(errorMessage);
}
```

> read more about: 
> - [array](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#arrays)
> - [Interface](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#interfaces)

### The alternative array syntax
### More about tsconfig
tsconfig with another rules:
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "noImplicitAny": true,
    "esModuleInterop": true,
    "moduleResolution": "node"
  }
}
```

### Adding Express to the mix
- install express: `npm install express`
- install type for express: `npm install --save-dev @types/express`
- install ts-node-dev: `npm install --save-dev ts-node-dev`
→ use to auto-reloading → improve work flow

- `package.json`:
```json
"scripts": {
    "ts-node": "ts-node",
    "multiply": "ts-node multiplier.ts",
    "calculate": "ts-node calculator.ts",
    "start": "ts-node index.ts",
    "dev": "ts-node-dev index.ts" // in case install ts-node-dev package for auto-reloading
  },
```
```ts
import express from 'express';
import { calculator2, Operation } from './calculate';

const app = express();

app.get('/ping', (_req, res) => {
  res.send('pong');
});

app.post('/calculate', (req, res) => {
  const {value1, value2, op} = req.body; /* no clue what the type will be */

  if ( !value1 || isNaN(Number(value1))) {
    res.status(400).send({ error: '...'});
  }

  const operation = op as Operation;
  const result  = calculator2(Number(value1), Number(value2), operation); 
  res.json({result});
});

const PORT = 3000;
app.listen(PORT , () => {
  console.log(`Server is running on port ${PORT}`);
  console.log('To test the server, visit http://localhost:3000/ping'
  );
});
```
> Note: entering module with `import`. If it not work, let's try combining method. `import ... = require('...')`

### The Horrors of any
About `any`
- Things become implicityly any type when one forgets to type functions.
- We can explicitly type things any. The only diff between the implicit and explicit any type is how the code look.
- config rule `noImplicitAny` on the compiler level → hightly recommend
- more things: req.body, res.body is explicitly typed any → so, ts don't complain about that (any type)
 
About `ESLint`: methods other than tsonfig.json to enforce a coding style. How to use ESlint to manage code
- install `ESlint` and its TS extensions: `npm install --save-dev eslint @eslint/js @types/eslint__js typescript typescript-eslint`
- setup `eslint.config.mjs`
```mjs
import eslint from '@eslint/js';
import tseslint from 'typescript-eslint';
import stylistic from "@stylistic/eslint-plugin";

export default tseslint.config({
  files: ['**/*.ts'],
  extends: [
    eslint.configs.recommended,
    ...tseslint.configs.recommendedTypeChecked,
  ],
  languageOptions: {
    parserOptions: {
      project: `./tsconfig.json`,
      tsconfigRootDir: import.meta.dirname,
    },
  },
  plugins: {
    "@stylistic": stylistic,
  },
  rules: {
    // 'no-console': 'warn',
    '@stylistic/semi': 'error',
    '@typescript-eslint/no-unsafe-assignment': 'off',
    '@typescript-eslint/no-explicit-any': ['error'],
    '@typescript-eslint/explicit-function-return-type': 'off',
    '@typescript-eslint/explicit-module-boundary-types': 'off',
    '@typescript-eslint/restrict-template-expressions': 'off',
    '@typescript-eslint/restrict-plus-operands': 'off',
    '@typescript-eslint/no-unsafe-argument': 'off',
    '@typescript-eslint/no-unused-vars': [
      'off',
      { 'argsIgnorePattern': '^_' }
    ],
  },
});
```
- setup `package.json`:
```json
"scripts": {
      "lint": "eslint ."
  },
```
- install and config `@stylistic/eslint-plugin`: `npm install --save-dev @stylistic/eslint-plugin`
→ lint complain if tring to define a var of type any

### Type assertion 
using type assertion is dirty trick that can be done to keep TS compiler and ESlint quite
- export the type
```ts
export type Operation = 'multiply' | 'add' | 'divide';
```
```ts
import { calculator, Operation } from './calculator';
app.post('/calculate', (req, res) => {
  // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
  const { value1, value2, op } = req.body;

  // validate the data here

  const result = calculator(
    // this is type assertion
    Number(value1), Number(value2), op as Operation
  );
  return res.send({ result });
});
```

> Read more here:
> - [disallow explicit any](https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/docs/rules/no-explicit-any.mdx)
> - [@typescript-eslint](https://github.com/typescript-eslint/typescript-eslint)
> - [type narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

## Typing An Express App
- setup: `npm init`
- install typescript: `npm install typescript --save-dev`
- config `package.json`:
```json
"scripts": {
  "tsc": "tsc"
},
```
- init tsconfig.json: `npm run tsc -- --init`
- config `tsconfig.json` like this:
```json
{
  "compilerOptions": {
    "target": "ES6",
    "outDir": "./build/",
    "module": "commonjs",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "esModuleInterop": true
  }
}
```
- install express: `npm install express`
- install @types/express, eslint:`npm install --save-dev eslint @eslint/js typescript-eslint @stylistic/eslint-plugin @types/express @types/eslint__js`

### Setting up the project
### Let there be code
### Implementing the functionality
### Node and JSON modules
### Utility Types
### Typing the Request and Response
### Preventing an accidental undefined result 
### Adding a new diary
### Validating requests 
### Type Guards
### Enum
### Using Schema Valiadation Libraries
### Parsing Request Body in Middleware

## Ref
- [console promp](https://github.com/TypeStrong/ts-node)
- [ts office playground](https://www.typescriptlang.org/play/index.html)
- [types in TS](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) → have to read
- [switch operation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
- [TypeScript Docs](https://www.typescriptlang.org/) → root
