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
we're not going to use `ts-node`. It's good one for sterting but in the long runk, should to use the official TS compiler that come with npm package.

### Setting Up the Project
`problem`: someone loves flying plane but has a difficult time managing his flight history
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
  - **target**: tells the compiler *which version to use when generating JS* 
  → use ES6 - be supported by most browser
  - **outDir**: tells *where the compiled code should be placed*.
  - **module**: tells the compiler that we want to *use CommonJS modules in the compiled code.* (can use `require` instead `import`)
  - [strict](https://www.typescriptlang.org/tsconfig/#strict)
  - some rules: 
    - [noImplicitAny](https://www.staging-typescript.org/tsconfig#noImplicitAny)
    - [read more here](https://www.staging-typescript.org/tsconfig#esModuleInterop)

<!--! install express, eslint, ts-node-dev -->
- install express: `npm install express`
- install @types/express, eslint:`npm install --save-dev eslint @eslint/js typescript-eslint @stylistic/eslint-plugin @types/express @types/eslint__js`
- create `eslint.config.mjs`:
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
      project: true,
      tsconfigRootDir: import.meta.dirname,
    },
  },
  plugins: {
    "@stylistic": stylistic,
  },
  rules: {
    '@stylistic/semi': 'error',
    '@typescript-eslint/no-unsafe-assignment': 'error',
    '@typescript-eslint/no-explicit-any': 'error',
    '@typescript-eslint/explicit-function-return-type': 'off',
    '@typescript-eslint/explicit-module-boundary-types': 'off',
    '@typescript-eslint/restrict-template-expressions': 'off',
    '@typescript-eslint/restrict-plus-operands': 'off',
    '@typescript-eslint/no-unused-vars': [
      'error',
      { 'argsIgnorePattern': '^_' }
    ],
  },
});
```
- setup dev env `ts-node-dev`: `npm install --save-dev ts-node-dev`
- update `package.json`
```json
"scripts": {
  "dev": "ts-node-dev index.ts",
  "lint": "eslint ."
},
```
- install `cors`: `npm i cors`
- `index.ts`
```ts
app.use(cors()); // to fix cors bug
```

### Let there be code
- implement `index.ts`: 
```ts 
import express from 'express';
const app = express();
app.use(express.json());

const PORT = 3000;

app.get('/ping', (_req, res) => {
  console.log('someone pinged here');
  res.send('pong');
});

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```
- create production build: `npm run tsc` 
→ build/index.js
- prevent compile files in the `build`-> eslint.config.mjs
```mjs
export default tseslint.config({
  // ...
  ignores: ["build/*"],
  // ...
});
```
- update `package.json`
```json
"scripts": {
  "start": "node build/index.js"
},
```

> note: need to defined the outDir in `tsconfig.json`

### Implementing the functionality
`problem`: diary entries info contain: date of the entry, weather , visibility, comment
```json
// example:
[
    {
    "id": 1,
    "date": "2017-01-01",
    "weather": "rainy",
    "visibility": "poor",
    "comment": "Pretty scary flight, I'm glad I'm alive"
  },
]
```

- how to structure source code
  - `src`
    - index.ts
    - `routes`
    - `controllers` 
    - `services`
    - `types`

- `src/routes/diaries.route.ts` → take care of all diary endpoints
```ts
import express from 'express';

const router = express.Router();

router.get('/', (_req, res) => {
  res.send('Fetching all diaries!');
});

router.post('/', (_req, res) => {
  res.send('Saving a diary!');
});

export default router;
```
- `index.ts`:
```ts
import express from 'express';
import diaryRouter from './routes/diaries';
const app = express();
app.use(express.json());

const PORT = 3000;

// ... do something here ...

app.use('/api/diaries', diaryRouter); // prefix /api/diaries 

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```
- fetch the data and save it to `src/data/entries.json` → (get data [here](../assets/p9.diaries-data.json))
- `business logic` saved into `services` → `src/service/diary.service.ts`
```ts
import diaryData from '../../data/entries.json';

const getEntries = () => {
  return diaryData;
};

const addDiary = () => {
  return null;
};

export default {
  getEntries,
  addDiary
};
```
- debug: `tsconfig.json`
```json
"compilerOptions": {
  "resolveJsonModule": true
}
```
- create `src/types/diary.type.ts`
```ts
// union type
export type Weather = 'sunny' | 'rainy' | 'cloudy' | 'windy' | 'stormy';
export type Visibility = 'great' | 'good' | 'ok' | 'poor';
// interface 
export interface DiaryEntry {
  id: number;
  date: string;
  weather: Weather;
  visibility: Visibility;
  comment: string;
}
```

- read more here:
  - [domain driven design](https://en.wikipedia.org/wiki/Domain-driven_design)
  - [spring framework](https://spring.io/)
  - [interface](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#interfaces)


### Node and JSON modules
<!-- read after -->
### Utility Types
- [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)
- [Omit](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys)
- [type alias](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)
```ts
// example `type alias`:
// in `src/types/diary.type.ts`
export type NonSensitiveDiaryEntry = Omit<DiaryEntry, 'comment'>;

// in `src/services/diary.service.ts`
//! NOT return diaries 
const getNonSensitiveEntries = (): NonSensitiveDiaryEntry[] => {
  return diaries;
};

/*
DO LIKE THIS
b/c: TS just check HAVE all required field or not, but excess fields are not prohibited ~ `comment` field
→ can return object (~type: DiaryEntry[]) but can access `comment` field 
→ *leaking the unwanted fields to the requesting browser* 
→ NEED exclude the fields by using `map`
*/
const getNonSensitiveEntries = (): NonSensitiveDiaryEntry[] => {
  return diaries.map(({ id, date, weather, visibility }) => ({
    id,
    date,
    weather,
    visibility,
  }));
};

// in `src/routes/diary.route.ts`
router.get('/', (_req, res) => {
  res.send(diaryService.getNonSensitiveEntries());
});
```

### Typing the Request and Response
<!-- read after -->
### Preventing an accidental undefined result 
```ts
// in `src/services/diary.service.ts`
/*
  problem: what the return value should be if an object is not found 
  → returned type: `DiaryEntry | undefined`
*/
const findById = (id: number): DiaryEntry | undefined => {
  const entry = diaries.find(d => d.id === id);
  return entry;
};

// in `src/routes/riary.route.ts`
router.get('/:id', (req, res) => {
  const diary = diaryService.findById(Number(req.params.id));

  if (diary) {
    res.send(diary);
  } else {
    res.sendStatus(404);
  }
});
```

### Adding a new diary
```ts
// in `src/routes/diary.route.ts`
router.post('/', (req, res) => {
  const { date, weather, visibility, comment } = req.body;
  const addedEntry = diaryService.addDiary(
    date,
    weather,
    visibility,
    comment,
  );
  res.json(addedEntry);
});

// in `src/services/diary.service.ts`
const addDiary = ( entry: NewDiaryEntry ): DiaryEntry => {
  const newDiaryEntry = {
    id: Math.max(...diaries.map(d => d.id)) + 1,
    ...entry
  };

  diaries.push(newDiaryEntry);
  return newDiaryEntry;
};

// in `src/types/diary.type.ts`
export type NewDiaryEntry = Omit<DiaryEntry, 'id'>;

/* 
  Do this to fix bug:
  - eslint-disable @typescript-eslint/no-unsafe-assignment 
*/
```

### Validating Requests
data from sources outsdie of our system cannot be fully trusted 
→ make decision `how to handle it?`
```ts
// example of risky when client send data to create new diary → MUST VALIDATE
const newDiaryEntry = diaryService.addDiary({
  date,
  weather,
  visibility,
  comment,
});

// in `src/routes/diary.route.ts`
router.post('/', (req, res) => {
  try {
    const newDiaryEntry = toNewDiaryEntry(req.body);

    const addedEntry = diaryService.addDiary(newDiaryEntry);
    res.json(addedEntry);
  } catch (error: unknown) {
    let errorMessage = 'Something went wrong.';
    if (error instanceof Error) {
      errorMessage += ' Error: ' + error.message;
    }
    res.status(400).send(errorMessage);
  }
})

// in `utils/toNewDiaryEntry.ts`
/*
  problems: what types of object? 
  - object: 
    + body of req
    + `type: any` (~defined by express)
    + idea of `toNewDiaryEntry`: map field of unknown → correct type AND check object that be defined as expected 
    → want to use `any` → using `unknown`
  - conclusion: 
    + using `unknown` is the ideal in case of **input validation** 
    + DON'T need to define the type to match any type
    + CAN first verify the type and confirm that is the expected type.
*/
const toNewDiaryEntry = (object : unknown): NewDiaryEntry => {
  const newEntry: NewDiaryEntry = {
    // ...
  };

  return newEntry;
};

/*
  eslint.config.mjs
  - can delete `no-unsafe-assignment`
*/
```

- read more about: 
  - [unknown](https://www.typescriptlang.org/docs/handbook/2/functions.html#unknown)

### Type Guards
```ts
// in `src/utils/toNewDiaryEntry.ts`
/*
  Objectives: creating parsers for each of the field of `object : unknown`
  1. validate comment: check comment exists AND ensure its type is string
  → parameters: type unknown → return comment (type string)
*/
const parseComment = (comment: unknown): string => {
  if (!comment || !isString(comment)) {
    throw new Error('Incorrect or missing comment');
  }
  return comment;
};

// string validate func ~ type guard func
/*
  this func return boolean AND have a `type predicate` as the return type 
  → predicate: `text is string` ~ text is parameter, string is ts type.
  → if func `isString` return `true` → compiler knos that parameter have type (ts type in predicate)
*/
const isString = (text: unknown): text is string => {
  return typeof text === 'string' || text instanceof String;
};

//! do the same thing with `date`, `weather`, `visibility` field
// date field
const isDate = (date: string): boolean => {
  return Boolean(Date.parse(date));
};

const parseDate = (date: unknown): string => {
  if (!date || !isString(date) || !isDate(date)) {
      throw new Error('Incorrect or missing date: ' + date);
  }
  return date;
};

// weather field
/*
  NOT good b/c: 
    + when update weather value have to update array → sus
    + hard to scale and maintain
  → SHOULD use `enum`
*/
const isWeather = (str: string): str is Weather => {
  return ['sunny', 'rainy', 'cloudy', 'stormy'].includes(str);
};

/*
  SHOULD use this one
*/
const isWeather = (param: string): param is Weather => {
  return Object.values(Weather).map(v => v.toString()).includes(param);
};

const parseWeather = (weather: unknown): Weather => {
  if (!weather || !isString(weather) || !isWeather(weather)) {
      throw new Error('Incorrect or missing weather: ' + weather);
  }
  return weather;
};

// visibility
const isVisibility = (param: string): param is Visibility => {
  return Object.values(Visibility).map(v => v.toString()).includes(param);
};

const parseVisibility = (visibility: unknown): Visibility => {
  if (!visibility || !isString(visibility) || !isVisibility(visibility)) {
      throw new Error('Incorrect or missing visibility: ' + visibility);
  }
  return visibility;
};
```
- read more about:
  - [type narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html) 

### Enum
```ts
// in `src/types/diary.type.ts`
export enum Weather {
  Sunny = 'sunny',
  Rainy = 'rainy',
  Cloudy = 'cloudy',
  Stormy = 'stormy',
  Windy = 'windy',
}

export enum Visibility {
  Great = 'great',
  Good = 'good',
  Ok = 'ok',
  Poor = 'poor',
}

// in `src/data/entries-date.ts`
/*
  problem: bug in "weather": "rainy"
  → b/c: CAN NOT assume a string is an enum
  → mapping init data TO DiaryEntry by using `src/utils/toNewDiaryEntry`
*/
const data = [
  {
      "id": 1,
      "date": "2017-01-01",
      "weather": "rainy", 
      "visibility": "poor",
      "comment": "Pretty scary flight, I'm glad I'm alive"
  },
]

const diaryEntries: DiaryEntry [] = data.map(obj => {
  const object = toNewDiaryEntry(obj) as DiaryEntry;
  object.id = obj.id;
  return object;
});

// in `src/utils/toNewDiaryEntry`
/*
  why using ~ if(`comment` in object && ...) ~ ?
  → b/c: if we don't have conditions → object is unknow AND unknown type does not allow any opperations, SO CAN'T access object's field
*/
  
const toNewDiaryEntry = (object: unknown): NewDiaryEntry => {
  if ( !object || typeof object !== 'object' ) {
    throw new Error('Incorrect or missing data');
  }

  if ('comment' in object && 'date' in object && 'weather' in object && 'visibility' in object)  {
    const newEntry: NewDiaryEntry = {
      weather: parseWeather(object.weather),
      visibility: parseVisibility(object.visibility),
      date: parseDate(object.date),
      comment: parseComment(object.comment)
    };

    return newEntry;
  }

  throw new Error('Incorrect data: some fields are missing');
};
```

- read more about:
  - `[in](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing)` operator 
  - [unknown](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type) type

### Using Schema Valiadation Libraries
- install zod: `npm i zod`
```ts
// in `src/utils/toNewDiaryEntry.ts` 
// lv1: using zod to replace parser
const parseComment = (comment: unknown): string => {
  return z.string().parse(comment);
};

// lv2: code simplification by using (zod enum, optional)
export const toNewDiaryEntry = (object: unknown): NewDiaryEntry => {
  if ( !object || typeof object !== 'object' ) {
    throw new Error('Incorrect or missing data');
  }

  if ('comment' in object && 'date' in object && 'weather' in object && 'visibility' in object)  {
    const newEntry: NewDiaryEntry = {
      weather: z.nativeEnum(Weather).parse(object.weather),
      visibility: z.nativeEnum(Visibility).parse(object.visibility),
      date: z.string().date().parse(object.date),
      comment: z.string().optional().parse(object.comment)
    };
    return newEntry;
  }
  throw new Error('Incorrect data: some fields are missing');
};

// lv3: define th whole new diary entry with `zod object`
const newEntrySchema = z.object({
  weather: z.nativeEnum(Weather),
  visibility: z.nativeEnum(Visibility),
  date: z.string().date(),
  comment: z.string().optional()
});

export const toNewDiaryEntry = (object: unknown): NewDiaryEntry => {
  return newEntrySchema.parse(object);
};

// in `src/routes/diary.route.ts and handle exception with `zod error`
router.post('/', (req, res) => {
  try {
    const newDiaryEntry = toNewDiaryEntry(req.body);
    const addedEntry = diaryService.addDiary(newDiaryEntry);
    res.json(addedEntry);

  } catch (error: unknown) {

    if (error instanceof z.ZodError) {
      res.status(400).send({ error: error.issues });
    } else {
      res.status(400).send({ error: 'unknown error' });
    }
  }
});

// in `src/types/diary.type.ts`
export interface DiaryEntry {
  id: number;
  date: string;
  weather: Weather;
  visibility: Visibility;
  comment?: string;
}
//OR 
export interface DiaryEntry extends NewDiaryEntry {
  id: number;
}
// infer the type from schema in `src/utils`
export type NewDiaryEntry = z.infer<typeof newEntrySchema>; 
```
- read more about `zod`:
  - [zod](https://zod.dev/)
  - [inferring types](https://zod.dev/?id=type-inference)
  - [optional](https://zod.dev/?id=optional)
  - [enum](https://zod.dev/?id=native-enums)
  - [date](https://zod.dev/?id=dates)
  - [string](https://zod.dev/?id=strings) 
  - [parse](https://zod.dev/?id=parse)
### Parsing Request Body in Middleware
```ts
// can REMOVE this method in `src/utils/toNewDiaryEntry`
export const toNewDiaryEntry = (object: unknown): NewDiaryEntry => {
  return newEntrySchema.parse(object);
};

// call dicrectly zod parser in `diary.route.ts`
router.post('/', (req, res) => {
  try {
    const addedEntry = diaryService.addDiary(newDiaryEntry); 
    const newDiaryEntry = NewEntrySchema.parse(req.body); // <<<=== call zod parser here
    res.json(addedEntry);

  } catch (error: unknown) {
    if (error instanceof z.ZodError) {
      res.status(400).send({ error: error.issues });
    } else {
      res.status(400).send({ error: 'unknown error' });
    }
  }
});

// OR validate input in middleware func `src/middlewares/newDiaryParser.ts`→ separate logic validation from the route handler
const newDiaryParser = (req: Request, _res: Response, next: NextFunction) => { 
  try {
    NewEntrySchema.parse(req.body);
    next();
  } catch (error: unknown) {
    next(error);
  }
};

/* 
  assign the correct type to req.body
  - req: params, res.body, req.body → type: unknown, unknown, NewDiaryEntry
  - res: return DiaryEntry
*/
router.post('/', newDiaryParser, (req: Request<unknown, unknown, NewDiaryEntry>, res: Response<DiaryEntry>) => {
  const addedEntry = diaryService.addDiary(req.body);
  res.json(addedEntry);
});

// handle Zod errors through a middleware.
const errorMiddleware = (error: unknown, _req: Request, res: Response, next: NextFunction) => { 
  if (error instanceof z.ZodError) {
    res.status(400).send({ error: error.issues });
  } else {
    next(error);
  }
};
```

## React with Types
advantages of TS in frontend dev: catch the following errors 
- pass an unwanted prop to a comp
- forgetting to pass a required prop
- passinng a prop with the wrong type

**let's start getting our hand dirty!!**

### Vite with TS
- init React proj: `npm create vite@latest frontend -- --template react-ts`
- run app: `npm run dev`
- `tsconfig.json`
  - strict: true
  - jsx: react-jsx 
  - lib: includes "type definitions for things found in browser env"

- `main.tsx`
```ts
// explain: ! make sure with TS that not null
ReactDOM.createRoot(document.getElementById('root')!).render(...);
```

read more about:
  - ["!" operator](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#non-null-assertion-operator-postfix-)
  - [lib](https://www.typescriptlang.org/tsconfig#lib)
 
### React Components with TS
- in JS, using PropTypes to check prop's type of comp
- in TS, DON'T NEED PropTypes → using interface to define type of prop

```tsx
/*
  - ts can infer the return type → `:JSX.Element` is optional
  - can using destructuring with inline types
*/
interface WelcomeProps {
  name: string;
}
const Welcome = (props: WelcomeProps): JSX.Element => {
  return <h1>Hello, {props.name}</h1>;
};
const Welcome = ({ name }: { name: string }) => <h1>Hello, {name}</h1>;
```

### Deeper Type Usage
- each type of part gets its own interface
```ts
// `kind` is a literal string used to narrow types later
interface CoursePartBasic { ... kind: "basic" }
interface CoursePartGroup { ... kind: "group" }
interface CoursePartBackground { ... kind: "background" }

// combine all types into a union
type CoursePart = CoursePartBasic | CoursePartGroup | CoursePartBackground;
```

- some benefit:
  - ts warns if a course part is missing required fields
  - `kind` let Ts automatically narrow to the right `subtype`
  - example: if a part says `kind: "basic"` but is missing description field → the editor complains

- dry-up code using inheritance
```ts
/*
  create base interface
*/
interface CoursePartBase {
  name: string;
  exerciseCount: number;
}

interface CoursePartBasic extends CoursePartBase {
  description: string;
  kind: "basic"
}

interface CoursePartGroup extends CoursePartBase {
  groupProjectCount: number;
  kind: "group"
}

interface CoursePartBackground extends CoursePartBase {
  description: string;
  backgroundMaterial: string;
  kind: "background"
}

type CoursePart = CoursePartBasic | CoursePartGroup | CoursePartBackground;

// `App.tsx`
const App = () => {
  const courseName = "Half Stack application development";
  const courseParts: CoursePart[] = [
    {
      name: "Fundamentals",
      exerciseCount: 10,
      description: "This is an awesome course part",
      kind: "basic"
    },
    {
      name: "Using props to pass data",
      exerciseCount: 7,
      groupProjectCount: 3,
      kind: "group"
    },
    {
      name: "Basics of type Narrowing",
      exerciseCount: 7,
      description: "How to go from unknown to string",
      kind: "basic"
    },
    {
      name: "Deeper type usage",
      exerciseCount: 14,
      description: "Confusing description",
      backgroundMaterial: "https://type-level-typescript.com/template-literal-types",
      kind: "background"
    },
  ]
}
```

- read more about:
  - [extend](https://www.typescriptlang.org/docs/handbook/2/objects.html#extending-types) 
  - [union](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types) 
  - [literal](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types)

### More Type Narrowing
Problem: How should we use these types in our components?
- TypeScript will only allow an operation (or attribute access) if it is valid for every member of the union.
- The solution: is to narrow the union with code 
(narrowing occurs when TS can deduce a more specific type for a value based on the structure of the code)
→ using `switch case` (~ can using `if`)
```ts
//  this pattern is called a discriminated union
courseParts.forEach(part => {
  switch(part.kind) {
    case "basic":
      console.log(part)
      break;
    case group: 
      console.log(part)
      break;
    case background: 
      console.log(part)
      break;
    default:
      break;
  }
});
```
- what if a new type is added?
  - If not handled explicitly, it falls into the `default` block silently.
  - Recommended: use [**exhaustive type checking**](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#exhaustiveness-checking) to catch missing cases
→ basic principle: if encounter unexpected value → calls func that accepts a value with type never AND return type [never](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-never-type)

```ts
/**
 * Helper function for exhaustive type checking
 */
const assertNever = (value: never): never => {
  throw new Error(
    `Unhandled discriminated union member: ${JSON.stringify(value)}`
  );
};
// replace `default` block
default:
  return assertNever(part);
```

- read more about: 
  - [type narrowing ](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
  - [discriminated union](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#discriminated-unions)
  - type [`never`](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-never-type)

### React App with State
```tsx
// App.ts
/*
  - useState in TypeScript is a `generic function` → type must be provided when it can't be inferred.
*/
interface Note {
  id: string,
  content: string
}


/*
  if we don't set type for `e`, so its type is `any` → err → using `:React.SyntheticEvent`
*/
const noteCreation = (e: React.SyntheticEvent) => {
    event.preventDefault()
    const noteToAdd = {
      content: newNote,
      id: String(notes.length + 1)
    }
    setNotes(notes.concat(noteToAdd));
    setNewNote('')
}

const App = () => {
  const [newNote, setNewNote] = useState('');
  const [notes, setNotes] = useState<Note[]>([]);

  return (
    <div>
      <form onSubmit={noteCreation}>
        <input
          value={newNote}
          onChange={(event) => setNewNote(event.target.value)} 
        />
        <button type='submit'>add</button>
      </form>
      <ul>
        {notes.map(note =>
          <li key={note.id}>{note.content}</li>
        )}
      </ul>
    </div>
  )
}
```

- read more about:
  - [form and event](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/forms_and_events)
  - [generic function](https://www.typescriptlang.org/docs/handbook/2/generics.html#working-with-generic-type-variables)
  - [useState](https://codewithstyle.info/Using-React-useState-hook-with-TypeScript/)
  - [inferred](https://www.typescriptlang.org/docs/handbook/type-inference.html#handbook-content)
  - [React TS Cheatsheet](https://react-typescript-cheatsheet.netlify.app/)

### Communication with the Server
- install `json-server`: `npm i json-server`
- update `package.json`
- create `data.json` for json-server
- run `json-server`: `npm run server`

- install axios: `npm i axios`

```ts 
export interface Note {
  id: string,
  content: string
}
export type NewNote = Omit<Note, 'id'>

const noteCreation = (event: React.SyntheticEvent) => {
  event.preventDefault()
  axios.post<Note>('http://localhost:3001/notes', { content: newNote })
    .then(response => {
      setNotes(notes.concat(response.data))
    })

  setNewNote('')
};

const App = () => {
  /* 
    fetch note data from server 
    using `axios.get<Note[]>().then(res=>res.data)` → res.data hava type~ Note[]
  */
  useEffect(() => {
    axios.get<Note[]>('http://localhost:3001/notes').then(response => {
      console.log(response.data); 
    })
  }, [])
}
```

```ts
// note.type.ts
export interface Note {
  id: string,
  content: string
}

export type NewNote = Omit<Note, 'id'>

// note.service.ts
const basuUrl = `http://localhost:3001/notes`

export const getAllNotes = () => {
  return axios
    .get<Note[]>(baseUrl)
    .then(response => response.data)
}

export const createNote = (object: NewNote) => {
  return axios
    .post<Note>(baseUrl, object)
    .then(response => response.data)
}
// App.tsx
  useEffect(() => {
    getAllNotes().then(data => {
      setNotes(data)
    })
  }, [])

  const noteCreation = (event: React.SyntheticEvent) => {
    event.preventDefault()
    createNote({ content: newNote }).then(data => {
      setNotes(notes.concat(data))
    })

    setNewNote('')
  };
```

read more about
- [How to use TS in React App](https://upmostly.com/typescript/how-to-use-axios-in-your-typescript-apps)

### A Note about Defining Object Types
- CAN define object types using either interface OR type alias. BOTH approaches are valid and often interchangeable.
- [recommend: using interface](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

| Comparison     | `interface`                        | `type`                                    |
| -------------- | ---------------------------------- | ----------------------------------------- |
| Name reuse     | Allows merging if names match      | Throws error if name is duplicated        |
| Extensibility  | Supports inheritance and extension | Limited to unions/intersections           |
| Recommendation | Preferred for object shapes        | Useful for unions, primitives, and tuples |

- read more about:
  - [interface](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#interfaces)
  - [type alias](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)
## Ref
- [console promp](https://github.com/TypeStrong/ts-node)
- [ts office playground](https://www.typescriptlang.org/play/index.html)
- [types in TS](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html) → have to read
- [switch operation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
- [TypeScript Docs](https://www.typescriptlang.org/) → root
