# Node.js and Express

## Simple web server
initial: `npm init`
pack.json 
```json
{
    "scripts": {
        "start": "node index.js"
    },
}
```
run server
    `node index.js` 
    `npm start`

OLD version
```jsx
    cosnt http = require('http')
```
## Express
install Express: `npm install express`
not important
    `npm install`
    `npm update`

## Web and express
NEW version
```jsx
    const express = require('express')
    const app = express()
    // init variable 

    app.get('/', (req, res) => {}) 

    const PORT =  3001
    app.listen(PORT, ()=> { console.log(`server running on port ${PORT}`)})
```
## nodemon
we don't have to restart the application to see the changes, if we make changes to the application's code

install nodemon: **`npm install nodemon`**
start nodemon: `node_modules/.bin/nodemon index.js`
start nodemon 2: pack.json
```json
{

  "scripts": {
    "dev": "nodemon index.js",
  }
}
```
and start with: `npm run dev`
## REST
## Fetching a single resource
```jsx
    app.get(`/api/notes/:id`, (res, req)=>{
        const id = Number(req.params.id)
        const note = notes.find(note => note.id === id)
        if( note){
            res.json(note)
        }else{
            res.status(404).end()
        }
    })
```
## Deleting resources
```jsx
    app.delete(`/api/notes/:id`,(res,req)=>{
        const id = Number(req.params.id)
        notes.filter(note => note.id !== id)
        res.status(204).end()
    })
```
## Postman
    can use curl or postman
## The Visual Studio REST client
    REST client plugin can be used instead Postman (use file .rest to test rest api)
## The WebStorm Http Client
    for IntelliJ WebStorm
## Receiving data 
    to access the data easily, we use json-parser
    
```jsx
    app.use(express.json())
```
    post method
```jsx
    const generateId = () = {
        // do smt
        return maxId + 1
    }

    app.post(`/api/notes`,(req, res) => {
        const body = req.body
        if(!body.content){
            return res.status(400).json({error: "content missing"})
        }
        cosnt note = {
            id: generateId(),
            content: body.content,
            important: body.important
        }
        notes = notes.concat(note)
        res.json(note)
    })
```
## About HTTP request types
## Middleware
request logger
```jsx  
    app.use('requestLogger') // must be use behind json-parser
    const requestLogger = (req,res, next) => {
        console.log('Method:', request.method)
        console.log('Path:  ', request.path)
        console.log('Body:  ', request.body)
        console.log('---')
        next()
    }
```

unknown endpoint 
```jsx 
    const unknownEndpoint = (req, res) => {
        res.status(404).send({errror:'unknown endponit'})
    }
    app.use (unknownEndpoint)
```

from exercises phonebook
install morgan: `npm install morgan`
config morgan
```jsx
    const morgan = require('morgan')
    morgan.token('body', function (req, res) { 
        return JSON.stringify(req.body)
    })
    const formatStr = ':method :url :status :res[content-length] - :response-time ms :body'
    app.use(morgan(formatStr))
```

# Deploying app to internet
## Same origin policy and CORS
`npm install cors`

## Application to the Internet
deploy with render

## Frontend production build 
production build: `npm run build`
## Serving static files from the backend
## The whole app to the internet 
## Straamlining deploying of the frontend
```json
{
  "scripts": {
    //...
    "build:ui": "rm -rf dist && cd ../frontend && npm run build && cp -r dist ../backend",
    "deploy:full": "npm run build:ui && git add . && git commit -m uibuild && git push"
  }
}
```

`npm config set script-shell "C:\\Program Files\\git\\bin\\bash.exe"`
[shx](https://www.npmjs.com/package/shx)
## Proxy

# Saving data to MongoDB
## Debuggin Node applications 
`nodemon --inspect index.js`
`node --inspeact index.js`
## MongoDB

uri mongo db `mongodb+srv://fullstack:thepasswordishere@cluster0.o1opl.mongodb.net/?retryWrites=true&w=majority`\
```js
const password = process.argv[2]
```
run:  `node mongo.js urPasswordHere`
install mongoose`npm install mongoose`
## Schema
## Creating and saving objects 
## Fetching objects from the daâbase
## Connecting the backend to adatabase
## Moving db configuration to it on module
define the value of env variable 
`MONGODB_URI=address_here npm run dev`

vip pro => can use .env
`npm install dotenv`
## Important note to Fly.io users
## Using database in route handlers
## kVerifying frontend and backend integration
## Error handling into middleware
## The orderof middle ware loading 
## Other operations 
## A true full stack developer's oath 

# Validation and ESLint
## Deploying the database backend to productions
## Lint 
install eslint `npm install eslint --save-dev`
config eslint `npx eslint --init`
intall plugin define set of code style rules `npm install --save-dev @stylistic/eslint-plugin-js`
check with: `npx eslint index.js` => check syntax of file index.js 

pack.json
```json
{
  "scripts": {
    "lint": "eslint ."
  },
}
```
check all file with: `npm run lint`
make file .eslintignore
```
dist
```

