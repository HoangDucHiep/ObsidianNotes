- `npm init`
``` json
{
  "name": "backend",
  "version": "0.0.1",
  "description": "",
  "main": "index.js",
  "scripts": {
	"start": "node index.js",    
	"dev": "node --watch index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
    },
  "author": "Matti Luukkainen",
  "license": "MIT"
}
```
- `npm install express`
- `npm update`
- `npm install`

``` js
const express = require('express')
const app = express()

let notes = [
  ...
]

app.get('/', (request, response) => {
  response.send('<h1>Hello World!</h1>')
})

app.get('/api/notes', (request, response) => {
  response.json(notes)
})

const PORT = 3001
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`)
})
```

#### REST
| URL      | verb   | functionality                                                 |
| -------- | ------ | ------------------------------------------------------------- |
| notes/10 | GET    | fetches a single resource                                     |
| notes    | GET    | fetches all resources in the collection                       |
| notes    | POST   | creates a new resource based on the request data              |
| notes/10 | DELETE | removes the identified resource                               |
| notes/10 | PUT    | replaces the entire identified resource with the request data |
| notes/10 | PATCH  | the identified resource with the request data                 |

#### endpoints
``` javascript
const express = require('express')
const app = express()
app.use(express.json())  // body parser

let notes = [
  ...
]

app.get('/', (request, response) => {
  response.send('<h1>Hello World!</h1>')
})

// GET ALL
app.get('/api/notes', (request, response) => {
  response.json(notes)
})

// GET BY ID
app.get('/api/notes/:id', (request, response) => {
  const id = request.params.id
  const note = notes.find(note => note.id === id)
  
  if (note) {
    response.json(note)
  } else {
    response.status(404).end()
  }
})

// DELETE
app.delete('/api/notes/:id', (request, response) => {
  const id = request.params.id
  notes = notes.filter(note => note.id !== id)

  response.status(204).end()
})

// ADD
const generateId = () => {
  const maxId = notes.length > 0
    ? Math.max(...notes.map(n => Number(n.id)))
    : 0
  return String(maxId + 1)
}

app.post('/api/notes', (request, response) => {
  const body = request.body

  if (!body.content) {
    return response.status(400).json({ 
      error: 'content missing' 
    })
  }

  const note = {
    content: body.content,
    important: body.important || false,
    id: generateId(),
  }

  notes = notes.concat(note)

  response.json(note)
})

const PORT = 3001
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`)
})
```
- it's possible to give a clue about the reason for sending a 404 error by [overriding the default NOT FOUND message](https://stackoverflow.com/questions/14154337/how-to-send-a-custom-http-status-message-in-node-express/36507614#36507614).

#### Middlewares
- Middleware is a function that receives three parameters:
```js
const requestLogger = (request, response, next) => {
  console.log('Method:', request.method)
  console.log('Path:  ', request.path)
  console.log('Body:  ', request.body)
  console.log('---')
  next()
}
```

- At the end of the function body, the _next_ function that was passed as a parameter is called. The _next_ function yields control to the next middleware.
- Middleware is used like this:
```js
app.use(requestLogger)
```


#### Deploying
- front end
```  js
import axios from 'axios'

const baseUrl = 'http://localhost:3001/api/notes'

const getAll = () => {
  const request = axios.get(baseUrl)
  return request.then(response => response.data)
}

// ...

export default { getAll, create, update }
```

#### Same origin policy and CORS
- `npm install cors`
```js
const cors = require('cors')
app.use(cors())
```

![[Pasted image 20250319094545.png]]

#### Frontend production build
- A production build for applications created with Vite can be created with the command [npm run build](https://vitejs.dev/guide/build.html).
![[Pasted image 20250319094654.png]]
- To make Express show _static content_, the page _index.html_ and the JavaScript, etc., it fetches, we need a built-in middleware from Express called [static](http://expressjs.com/en/starter/static-files.html).
- When we add the following amidst the declarations of middlewares
```js
app.use(express.static('dist'))
```
```js
import axios from 'axios'
const baseUrl = '/api/notes'
const getAll = () => {
  const request = axios.get(baseUrl)
  return request.then(response => response.data)
}

// ...
```

``` json
{
  "scripts": {
    // ...
    "build:ui": "@powershell Remove-Item -Recurse -Force dist && cd ../frontend && npm run build && @powershell Copy-Item dist -Recurse ../backend",
    "deploy": "fly deploy",
    "deploy:full": "npm run build:ui && npm run deploy",    
    "logs:prod": "fly logs"
  }
}
```

#### Proxy
- Because in development mode the frontend is at the address _localhost:5173_, the requests to the backend go to the wrong address _localhost:5173/api/notes_. The backend is at _localhost:3001_.
- If the project was created with Vite, this problem is easy to solve. It is enough to add the following declaration to the _vite.config.js_ file of the frontend directory.
``` js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
      proxy: {
          '/api': {
                target: 'http://localhost:3001',
                changeOrigin: true,      
            },    
        }  
    },
})
```


### MongoDB
- `npm install mongoose`
- mongo.js
``` js
const mongoose = require('mongoose')

if (process.argv.length < 3) {
  console.log('give password as argument')
  process.exit(1)
}

const password = process.argv[2]

const url = `mongodb+srv://fullstack:${password}@cluster0.a5qfl.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0`

mongoose.set('strictQuery',false)

mongoose.connect(url)

const noteSchema = new mongoose.Schema({
  content: String,
  important: Boolean,
})

const Note = mongoose.model('Note', noteSchema)

const note = new Note({
  content: 'HTML is easy',
  important: true,
})

/*Note.find({}).then(result => {
  result.forEach(note => {
    console.log(note)
  })
  mongoose.connection.close()
})*/

note.save().then(result => {
  console.log('note saved!')
  mongoose.connection.close()
})
```


#### needed packages
``` json
"scripts": {
    "start": "cross-env NODE_ENV=production node index.js",
    "dev": "cross-env NODE_ENV=development node --watch index.js",
    "test": "cross-env  NODE_ENV=test node --test",
    "lint": "eslint ."
},

"dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.4.1",
    "express": "^4.18.2",
    "mongoose": "^8.1.1"
  },

"devDependencies": {
    "@flydotio/dockerfile": "^0.5.0",
    "@stylistic/eslint-plugin-js": "^1.6.1",
    "cross-env": "^7.0.3",
    "eslint": "^8.56.0",
    "nodemon": "^3.0.3",
    "supertest": "^7.0.0"
}
```

