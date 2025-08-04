

# Structure of backend
***file***
- index.js
```js
    const app = require('./app')
    const config = require('./utils/config')
    const logger = require('./utils/logger')

    app.listen(config.PORT, () => {
    logger.info(`Server running on port ${config.PORT}`)
    })
```
- app.js
```js
    const config = require('./utils/config')
    const express = require('express')
    const app = express()
    const cors = require('cors')
    const notesRouter = require('./controllers/NotesRouter')
    const usersRouter = require('./controllers/UsersRouter')
    const loginRouter = require('./controllers/LoginRouter')
    const middleware = require('./utils/middleware')
    const logger = require('./utils/logger')
    require('express-async-errors')

    const mongoose = require('mongoose')


    mongoose.set('strictQuery', false)
    logger.info('connecting to ', config.MONGODB_URI)
    mongoose.connect(config.MONGODB_URI)
        .then(()=> {
            logger.info('connected to MongoDB')
        })
        .catch((err) => {
            logger.error(`error connecting to MongoDB: ${err.message}`)
        })

    app.use(cors())
    app.use(express.static('dist'))
    app.use(express.json())
    app.use(middleware.requestLogger)

    app.use('/api/notes', notesRouter)
    app.use('/api/users', usersRouter)
    app.use('/api/login', loginRouter)
    app.use(middleware.unknownEndpoint)
    app.use(middleware.errorHandler)

    module.exports = app
```

***pack***
- dist (npm run deploy:full) => fe production

- controllers
[router in express](http://expressjs.com/en/api.html#router)
the router is in fact a middleware, that can be used for defining "related routes" in a single place
```js
// LoginRouter.js
    const User = require('userModel')
    const loginRouter = require('express').Router()

    loginRouter.post('/', async (req,res)=> {})
    module.exports = loginRouter

//  UserRouter.js
    const bcrypt = require('bcrypt')
    const usersRouter = require('express').Router()
    const User = require('../models/userModel')

    usersRouter.get('/', async(req, res)=> {
        res.json(users)
    })
    userRouter.post('/', async (req,res)=>{
        res.status(201).json(savedUser)
    })
    module.exports = UserRouter

//  NotesRouter.js
    const notesRouter = require('express').Router()
    const jwt = require('jsonwebtoken')
    const Note = require('../models/noteModel')
    const User = require('../models/userModel')

    notesRouter.get('/', async (req, res)=>{})
    notesRouter.get('/:id', async (req, res)=>{})
    notesRouter.post('/', async (req, res)=>{})
    notesRouter.delete('/', async (req, res)=>{})
    notesRouter.put('/', async (req, res)=>{})

    module.exports = NoteRouter
```
- models
```js
// noteModel.js
    const mongoose = require('mongoose')
    const noteSchema = new mongoose.Schema({
        content: {},
        important: Boolean,
        user: {}
    })     
    noteSchema.set('toJSON',{config smt here}) 
    const Note = mongoose.model('Note',noteSchema)
    module.exports = Note

// userModel.js
    const mongoose = require('mongoose')
    const userSchema = new  mongoose.Schema({
        username:{},
        name: String,
        passwordHash: String,
        notes:[]
    })
    userSchema.set('toJSON', {config})    
    const User = mongoose.model('User', userSchema)
    module.exports = User    
```

- utils
external loggin service: [graylog](https://www.graylog.org/), [papertrail](https://papertrailapp.com/)
```js
// config.js
    require('dotenv').config()
    const PORT = process.env.PORT
    const MONGODB_URI = process.env.NODE_ENV
    module.exports = {MONGODB_URI, PORT}

//   logger.js
    const info = (...params) => {console.log(...params)}
    const error = (...params) => {console.error(...params)}
    module.exports = {info,error}

// middleware.js
    const logger = require('logger')
    const requestLogger = (req, res, next) =>{}
    const morgan ... do smt
    const unknownEndpoint = (req, res) =>{res.status(404).send{(error: 'unknown endpoint')}}
    const errorHandler = (err, req, res, next) =>{}
    module.exports = {requestLogger, unknownEndpoint, errorHandler}
```

***npm***
- package.json
- package-lock.json
  
***extra***
- tests 
  - userapi.test.js
- request
  - testapi.rest

## something about test
`npm install cross-env`
`npm install --save-dev cross-env`

help us write tests for testing api
`npm install --save-dev supertest`

optional 
`npm test -- --test-only`

##  (VERY IMPORTANT) async/await 
NEED CHECK ONE MORE TIME

## eliminating the try-catch
use library: `npm install express-async-errors`
## something idk
- [strictEqual](https://nodejs.org/docs/latest/api/assert.html#assertstrictequalactual-expected-message)
# Structure of frontend
- components
```jsx
// Togglabel
```

- services
```js
// LoginService
// NoteService
```

- App.jsx
```jsx
    const App = () => {
        
    }
```
# User administration
- relation between User - Note is 1 - n
- relational databases: id user can be saved like foreign key in note table 
- document databases: 

- Create User: 
  - don't save password raw -> use oneway hash to make password hash
`npm install bcrypt` <!--! use to hash password -->

```js
usersRouter.post('/', async (request, response) => {
  const { username, name, password } = request.body

  const saltRounds = 10
  const passwordHash = await bcrypt.hash(password, saltRounds) // hash pw with bcrypt.hash()

  const user = new User({
    username,
    name,
    passwordHash,
  })

  const savedUser = await user.save()

  response.status(201).json(savedUser)
})
```

## Populate 
[populate](http://mongoosejs.com/docs/populate.html)

try this code and explain
```js
    userRouter.get('/', async (req, res) => {
        const user = await User.find({}).populate('notes')
    })
```

select fields: 
```js
    usersRouter.get('/', async (request, response) => {
    const users = await User
        .find({}).populate('notes', { content: 1, important: 1 })
    response.json(users)
    })
```


# Token authentication
[img](https://fullstackopen.com/static/259c9dce6b3d1d77bedb04e799ac7dd3/5a190/16new.png)
![alt text](image-2.png)

make json web token, install lib
`npm install jsonwebtoken`

check login
```js
    const user = await User.findOne({ username })
    const passwordCorrect = user === null
        ? false
        : await bcrypt.compare(password, user.passwordHash)
    if(!(user && passwordCorrect)) return res.status(401).json({error: 'invalil username or passwrod'})
```
```js
  const userForToken = {
    username: user.username,
    id: user._id,
  }

  const token = jwt.sign(userForToken, process.env.SECRET) // if username, password are correct, token be made by method jwt.sign()
```

## Limiting  creating  new notes  to logged in users
## Problem of Token based authentication
## End notes