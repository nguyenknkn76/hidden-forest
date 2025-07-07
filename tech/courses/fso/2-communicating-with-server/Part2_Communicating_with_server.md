  - [Couple of important remarks](#couple-of-important-remarks)

**Main content**
- How to render a data colleciton, like a list of names to the screen 
- How a user can submit data to React app using html form s 
- How JS code in the browser can fetch and handle data stored in a remote backend server 
- Few simple ways of adding CSS styles to React app 

rookie: newbie, tân binh 

# Rendering a collection, modules
## console.log
Read again [debugging react app](https://fullstackopen.com/en/part1/a_more_complex_state_debugging_react_apps#debugging-react-applications)
## Protip: VSCode snippets
(optionals) - (not important)
Protip: Mẹo 
Same: sout in Neatbeans
Creating [snippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_creating-your-own-snippets) in VSCode
Creating snippets with [VScode plugin](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)
Some [extension](https://marketplace.visualstudio.com/search?term=console.log&target=VSCode&category=All%20categories&sortBy=Relevance) for debugging with console.log()

## JavaScript Arrays
Some info about JS [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
Some basic method:
- find
- map
- filter

Youtube source: [Functional Programming in JS](https://www.youtube.com/playlist?list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84) 
- [Higher order functions](https://www.youtube.com/watch?v=BMUiFMZr7vk&list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84)
- [Map](https://www.youtube.com/watch?v=bCqtb-Z5YGQ&list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84&index=2)
- [Reduce basics](https://www.youtube.com/watch?v=Wl98eZpkp-c&t=31s)

## Event Handlers Revisited
[Event handling rebisited](https://fullstackopen.com/en/part1/a_more_complex_state_debugging_react_apps#event-handling-revisited)
[Passing evenet hadlers to child comps](https://fullstackopen.com/en/part1/a_more_complex_state_debugging_react_apps#passing-event-handlers-to-child-components)

## Rendering Collections 
## Key attribute
[Keeping list items in order with key](https://react.dev/learn/rendering-lists#keeping-list-items-in-order-with-key)
[Reseting sate with a key](https://react.dev/learn/preserving-and-resetting-state#option-2-resetting-state-with-a-key)

## Map
Some info about method [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

## Anti pattern: Array Indexes as Keys
Find more info in this [article](https://robinpokorny.medium.com/index-as-a-key-is-an-anti-pattern-e0349aece318)

## Refactoring Modules
[Structuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) 
[Import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) 
[Export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) 

## When the Applicaiton Breaks 
## Web dev's oath

# Forms
## Saving the notes in the component state
[useState](https://react.dev/reference/react/useState) function
[Web form building blocks](https://developer.mozilla.org/en-US/docs/Learn/Forms)
[Responding to event](https://react.dev/learn/responding-to-events)
[HTMLFormElement: submit event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit_event)
NB: Use event.preventDefault() method to prevent the default action of submitting a form 

## Controlled component
[Controlled comps ](https://react.dev/reference/react-dom/components/input#controlling-an-input-with-a-state-variable) with onChange function
Add new items into arr with [concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) method
Why we must use concat: [never mutate state directly](https://react.dev/learn/updating-objects-in-state#why-is-mutating-state-not-recommended-in-react)

## Filtering Displayed Elements
[Conditional](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) operator 
Filtering arr with the help of the arr [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) method
[Equality comparisons and sameness](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness) (Compare " === " and " == ")

## Some important knowleadge
- Handling JS arrays [method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) 
- [Why It's So Hard to Check Object Equality in JavaScript](https://www.joshbritz.co/posts/why-its-so-hard-to-check-object-equality/)
- [Alert](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert) method





# Getting data from server
Tool: [JSson server](https://github.com/typicode/json-server)
- install json-server: `npm install -g json-server`
- run json-server: `json-server --port 3001 --watch db.json`
- run json-server from root directory of app: `npx json-server --port 3001 --watch db.json`
- url: http://localhost:3001/notes

Format the display of json data in browser with [JSONVue](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc)

## The browser as a runtime environment
>[ MUST READ AGAIN IN FULL STACK OPEN](https://fullstackopen.com/en/part2/getting_data_from_server#:~:text=Tr%C3%ACnh%20duy%E1%BB%87t%20l%C3%A0%20m%C3%B4i%20tr%C6%B0%E1%BB%9Dng%20th%E1%BB%9Di%20gian%20ch%E1%BA%A1y)

Old way: fetch data with XMLHttpRequest (http request made using an XHR object) (NOT recommended)
Now: [fetch](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch) method (support by browsers) with [promisses](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

JS engines or runtime env follow the [asynchoronous model](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
Synchorous is code be excuted from top to bottom >< Asynchronous 
All [IO operations](https://en.wikipedia.org/wiki/Input/output) (with some exceptions) to be executed as non-blocking. This means that code execution continues immediately after calling an IO function, without waiting for it to return.

Currently, JavaScript engines are single-threaded, which means that they cannot execute code in parallel. As a result, it is a requirement in practice to use a non-blocking model for executing IO operations. Otherwise, the browser would "freeze" during, for instance, the fetching of data from a server.

[What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
[Web workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) 
[Single thread](https://medium.com/techtrument/multithreading-javascript-46156179cf9a)

## npm
Get data from server with function [fetch](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch) 
Use library [axios](https://github.com/axios/axios) to communication between server and browser
Some info about [npm](https://docs.npmjs.com/about-npm) 
***Install axios***
- `npm istall axios`

***Install json-server***
- `npm install json-server --save-dev`
- in pack.json:
```json
  "scripts": {
    "server": "json-server -p3001 --watch db.json"
  }
```
- start json-server: `npm run server`

[Differences between `npm install axios` and `npm install json-server --save-dev`](https://fullstackopen.com/en/part2/getting_data_from_server#:~:text=There%20is%20a%20fine,part%20of%20the%20course.)

*NB: npm-commands should always be run in the project root directory, which is where the package.json file can be found.*

## Axios and promises
*NB: To run json-server and your react app simultaneously, you may need to use two terminal windows. One to keep json-server running and the other to run our React application.*
in main.jsx: 
```js
import axios from 'axios'
```
url: http://localhost:5173/

Axios's get method returns a [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises) 
A promise is an object representing the eventual completion or failure of an asynchromous operation. A promise can have three distinct states:
- pending 
- fullfilled 
- rejected

## Effect hooks 
[State hooks](https://react.dev/learn/state-a-components-memory)
[Effect hooks ](https://react.dev/reference/react/hooks#effect-hooks) (be used when fetch data from server)


*Effects let a component connect to and synchronize with external systems. This includes dealing with network, browser DOM, animations, widgets written using a different UI library, and other non-React code.*

[useEffect](https://react.dev/reference/react/useEffect) takes two parameters. The first is a function, the effect itself [specify how often the effect is run ](https://react.dev/reference/react/useEffect#parameters)
*By default, effects run after every completed render, but you can choose to fire it only when certain values have changed.*
## The dev runtime env 
The makeup of the application
![alt text](image-1.png)

The JavaScript code making up our React application is run in the browser. The browser gets the JavaScript from the React dev server, which is the application that runs after running the command npm run dev. The dev-server transforms the JavaScript into a format understood by the browser. Among other things, it stitches together JavaScript from different files into one file. We'll discuss the dev-server in more detail in part 7 of the course.

The React application running in the browser fetches the JSON formatted data from json-server running on port 3001 on the machine. The server we query the data from - json-server - gets its data from the file db.json.

At this point in development, all the parts of the application happen to reside on the software developer's machine, otherwise known as localhost. The situation changes when the application is deployed to the internet. We will do this in part 3.

# Altering data inserver
## REST
routes 
```txt
GET    /posts
GET    /posts/:id
POST   /posts
PUT    /posts/:id
PATCH  /posts/:id
DELETE /posts/:id
# Same for comments
```

run json-server from root folder: `npx json-server --port 3001 --watch db.json`
## Sending data to the server
## Changing the importance of notes
## Extracting communication with the backend into separate module
## Cleaner syntax for defining object literals 
## Promises and Errors
## Full stack dev's oath

# Adding styles to React app
## Improved error msg
## Inline styles
## Couple of important remarks 
