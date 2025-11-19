# Node.js Quick Reference (Hapi + Express)

A clean, simple, ready‑to‑paste MD file covering Node.js basics, Express, and Hapi with simple explanations and examples.

---

# 1. What is Node.js?

Node.js is a **JavaScript runtime** that lets you run JS on the server. It is built on Chrome’s V8 engine.

* Non‑blocking I/O
* Event‑driven architecture
* Perfect for APIs and real‑time apps

---

# 2. Package Manager (npm / yarn)

### Initialize Project

```javascript
npm init -y
```

### Install Packages

```javascript
npm install express
npm install @hapi/hapi
```

### Run Project

```javascript
node index.js
```

---

# 3. Common Node.js Core Modules

* `fs` – File system
* `path` – Path utilities
* `os` – System info
* `http` – Create raw server
* `events` – Event emitter

Example:

```javascript
const fs = require('fs');
fs.readFile('file.txt', 'utf8', (err, data) => console.log(data));
```

---

# 4. Express.js Basics

A minimal and popular web framework.

### Create Server

```javascript
const express = require('express');
const app = express();
app.use(express.json());

app.get('/', (req, res) => {
  res.send('Hello from Express');
});

app.listen(3000, () => console.log('Server running'));
```

### Routes

```javascript
app.post('/users', (req, res) => {
  res.json({ message: 'User created', data: req.body });
});
```

### Middleware

```javascript
app.use((req, res, next) => {
  console.log('Request received');
  next();
});
```

---

# 5. Hapi.js Basics

A rich framework with built‑in validation and configuration.

### Create Server

```javascript
const Hapi = require('@hapi/hapi');

const init = async () => {
  const server = Hapi.server({ port: 3000, host: 'localhost' });

  server.route({
    method: 'GET',
    path: '/',
    handler: () => 'Hello from Hapi'
  });

  await server.start();
  console.log('Server running');
};

init();
```

### Route with Payload

```javascript
server.route({
  method: 'POST',
  path: '/users',
  handler: (req, h) => ({ message: 'User created', data: req.payload })
});
```

### Validation Example (Joi)

```javascript
const Joi = require('joi');

server.route({
  method: 'POST',
  path: '/login',
  options: {
    validate: {
      payload: Joi.object({
        username: Joi.string().required(),
        password: Joi.string().min(6).required()
      })
    }
  },
  handler: (req, h) => 'Login success'
});
```

---

## 6. Express vs Hapi (Simple)

| Feature        | Express                       | Hapi                               |
| -------------- | ----------------------------- | ---------------------------------- |
| Setup          | Minimal & flexible            | Structured & configuration-focused |
| Routing        | Lightweight                   | Strong & rule-driven               |
| Validation     | External libs (Joi, Yup)      | Built-in Joi integration           |
| Plugins        | Middleware ecosystem          | Strong plugin system               |
| Learning Curve | Easier for beginners          | Slightly higher                    |
| Best For       | Quick APIs, small–medium apps | Large-scale, enterprise-grade APIs |

### When to Choose Express

* You want **fast setup** and fewer rules.
* Your project is **small or medium-sized**.
* You prefer **flexible routing** and **middleware freedom**.
* You want a **wide community ecosystem**.
* You need to prototype APIs quickly.

### When to Choose Hapi

* You want **strict validation**, **schemas**, structured configuration.
* Enterprise apps needing **security-first design**.
* You want **built-in input validation** without many external libraries.
* You work on **large-scale APIs** requiring clear boundaries.
* You need a **plugin-driven, rule-based** architecture.
---

# 7. Environment Variables

```javascript
npm install dotenv
```

```javascript
require('dotenv').config();
console.log(process.env.PORT);
```

---

# 8. Error Handling

### Express

```javascript
app.use((err, req, res, next) => {
  res.status(500).json({ error: err.message });
});
```

### Hapi

```javascript
server.ext('onPreResponse', (req, h) => {
  const error = req.response;
  if (error.isBoom) return h.response({ error: error.message }).code(error.output.statusCode);
  return h.continue;
});
```

---

# 9. Async/Await in Node

```javascript
const fetchUser = async () => {
  return { name: 'Mani' };
};

(async () => {
  const user = await fetchUser();
  console.log(user);
})();
```

---

# 10. File Handling

```javascript
const fs = require('fs');

fs.writeFileSync('a.txt', 'Hello');
console.log(fs.readFileSync('a.txt', 'utf8'));
```

---

# 11. Basic Project Folder Structure

```
project/
 ├── src/
 │    ├── routes/
 │    ├── controllers/
 │    ├── services/
 │    └── app.js
 ├── package.json
 └── README.md
```

---

# 12. Ready‑to‑Use Express API Boilerplate

```javascript
const express = require('express');
const app = express();
app.use(express.json());

app.get('/health', (req, res) => res.send('OK'));

app.listen(4000, () => console.log('API ready'));
```

---

# 13. Ready‑to‑Use Hapi API Boilerplate

```javascript
const Hapi = require('@hapi/hapi');

const init = async () => {
  const server = Hapi.server({ port: 4000, host: 'localhost' });

  server.route({ method: 'GET', path: '/health', handler: () => 'OK' });

  await server.start();
  console.log('API ready');
};

init();
```

---

# 14. PM2 (Process Manager)

PM2 keeps Node apps alive, auto restarts, and manages logs.

### Install PM2

```javascript
npm install pm2 -g
```

### Start App

```javascript
pm2 start app.js
```

### Monitor

```javascript
pm2 monit
```

### Save Process List

```javascript
pm2 save
```

### Restart All

```javascript
pm2 restart all
```

---

# 15. JWT Authentication (Simple & Explained)

JWT (JSON Web Token) is a secure way to send user data between client and server.
A JWT has **three parts separated by dots (`.`):**

### 1. Header

Contains metadata like type of token and algorithm.

```javascripton
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### 2. Payload

Contains user data (claims).

```javascripton
{
  "id": 1,
  "name": "Mani",
  "exp": 1735689600
}
```

### 3. Signature

Used to verify token integrity.

```
HMACSHA256( base64UrlEncode(header) + "." + base64UrlEncode(payload), SECRET_KEY )
```

### Final Token Format

```
HEADER.PAYLOAD.SIGNATURE
```

Example:

```
eyJhbGciOiJIUzI1NiIs...eyJpZCI6MX0...iE3as89Klsal0
```

---

### Install JWT

```javascript
npm install jsonwebtoken
```

### Generate Token

```javascript
const jwt = require('jsonwebtoken');

const token = jwt.sign(
  { id: 1, role: 'admin' },
  'SECRET_KEY',
  { expiresIn: '1h' }
);
```

### Verify Token Middleware

```javascript
const auth = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) return res.status(401).json({ error: 'Missing token' });

  try {
    req.user = jwt.verify(token, 'SECRET_KEY');
    next();
  } catch (err) {
    res.status(401).json({ error: 'Invalid or expired token' });
  }
};
```

---

# 16. Rate Limiting

### Express (Using express-rate-limit)

```javascript
npm install express-rate-limit
```

```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 1 * 60 * 1000, // 1 minute
  max: 10 // 10 requests per minute
});

app.use('/api', limiter);
```

### Hapi Rate Limiting (Using plugin hapi-rate-limit)

```javascript
await server.register({
  plugin: require('hapi-rate-limit'),
  options: {
    userLimit: 10,
    userCache: { expiresIn: 60000 }
  }
});
```

---

# 17. Clustering in Node.js

Clustering allows Node.js to use **multiple CPU cores** to handle high traffic.

### Example: Simple Cluster Setup

```javascript
const cluster = require('cluster');
const os = require('os');

if (cluster.isPrimary) {
  const cores = os.cpus().length;
  console.log('Master process running');

  for (let i = 0; i < cores; i++) cluster.fork();

  cluster.on('exit', () => {
    console.log('Worker crashed, restarting...');
    cluster.fork();
  });

} else {
  require('./server'); // Your API
}
```

---

# 18. Worker Threads

Worker threads allow CPU‑heavy tasks to run **without blocking** the main event loop.

### Example Worker

**worker.js:**

```javascript
const { parentPort } = require('worker_threads');

let result = 0;
for (let i = 0; i < 1e9; i++) result += i;

parentPort.postMessage(result);
```

**main.js:**

```javascript
const { Worker } = require('worker_threads');

const worker = new Worker('./worker.js');

worker.on('message', result => console.log('Result:', result));
```

Use worker threads when:

* Doing heavy CPU computations
* Parsing very large JSON
* Processing images/files
* Encryption/decryption

---

# 19. Redis Caching

Redis is an in‑memory key-value store used for caching and fast lookups.

### Install Redis Client

```javascript
npm install redis
```

### Connect to Redis

```javascript
const redis = require('redis');
const client = redis.createClient();

client.connect();
```

### Set & Get Cache

```javascript
// Set value
await client.set('user:1', JSON.stringify({ name: 'Mani' }), { EX: 60 }); // expires in 60 sec

// Get value
const data = await client.get('user:1');
console.log(JSON.parse(data));
```

### Caching API Response Example

```javascript
app.get('/users/:id', async (req, res) => {
  const id = req.params.id;
  const cacheKey = `user:${id}`;

  const cached = await client.get(cacheKey);
  if (cached) return res.json(JSON.parse(cached));

  const user = await getUserFromDB(id);
  await client.set(cacheKey, JSON.stringify(user), { EX: 120 });

  res.json(user);
});
```

---

# 20. Popular Hapi Plugins

Hapi has a strong plugin ecosystem for modular development.

### 1. **@hapi/inert** – Static File Serving

```javascript
await server.register(require('@hapi/inert'));
```

### 2. **@hapi/vision** – Templating

```javascript
await server.register(require('@hapi/vision'));
```

### 3. **hapi-auth-jwt2** – JWT Authentication

```javascript
await server.register(require('hapi-auth-jwt2'));

server.auth.strategy('jwt', 'jwt', {
  key: 'SECRET_KEY',
  validate: async (decoded) => ({ isValid: true })
});

server.auth.default('jwt');
```

### 4. **hapi-rate-limit** – Rate Limiting

```javascript
await server.register({
  plugin: require('hapi-rate-limit'),
  options: { userLimit: 20 }
});
```

### 5. **Good** – Logging

```javascript
await server.register({
  plugin: require('@hapi/good'),
  options: {
    reporters: {
      console: [{ module: '@hapi/good-console' }, 'stdout']
    }
  }
});
```

### 6. **Bell** – OAuth Login (Google, Facebook)

```javascript
await server.register(require('@hapi/bell'));
```

---
