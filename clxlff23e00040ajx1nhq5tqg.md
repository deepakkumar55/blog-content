---
title: "Understanding JWT Authentication: A Complete Guide"
seoTitle: "JWT Authentication: Complete Guide"
seoDescription: "Complete guide to implementing JWT authentication in a MERN stack application, covering setup, user model creation, and route protection"
datePublished: Wed Jun 19 2024 06:02:29 GMT+0000 (Coordinated Universal Time)
cuid: clxlff23e00040ajx1nhq5tqg
slug: jwt-authentication
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718761770433/072d3694-f3e5-4359-ad77-e6a1f061b218.jpeg
tags: express, productivity, project, programming-blogs, js, javascript, json, opensource, mongodb, nodejs, projects, jwt, reactjs, expressjs-cilb5apda0066e053g7td7q24, json-web-tokens-jwt

---

Authentication is a critical aspect of web development, ensuring secure access to resources and protecting sensitive data. JSON Web Tokens (JWT) have become a popular choice for handling authentication in modern web applications due to their simplicity and security. In this step-by-step guide, we'll walk through implementing JWT authentication in a MERN stack application.

## What is JWT?

JSON Web Token (JWT) is an open standard (RFC 7519) for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.

## Key Concepts of JWT

1. **Header**: Contains metadata about the token, including the type of token and the signing algorithm.
    
2. **Payload**: Contains the claims, which are statements about an entity (typically, the user) and additional data.
    
3. **Signature**: Ensures that the token hasn't been altered. It is created by encoding the header and payload and signing them using a secret key or a public/private key pair.
    

## Step-by-Step Guide to Implement JWT Authentication

### Step 1: Setting Up Your MERN Stack

Ensure you have the following setup:

* **MongoDB** for the database
    
* **Express** for the server framework
    
* **React** for the front-end
    
* **Node.js** for the runtime environment
    

### Step 2: Install Necessary Packages

Start by installing the required packages using npm:

```bash
npm install express mongoose jsonwebtoken bcryptjs cors body-parser
```

### Step 3: Set Up the Server

Create a new file `server.js` and set up a basic Express server:

```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const bodyParser = require('body-parser');

const app = express();

// Middleware
app.use(cors());
app.use(bodyParser.json());

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/yourdbname', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

const db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', () => {
  console.log('Connected to MongoDB');
});

app.listen(5000, () => {
  console.log('Server is running on port 5000');
});
```

### Step 4: Create User Model

Create a `User` model with Mongoose:

```javascript
const mongoose = require('mongoose');
const bcrypt = require('bcryptjs');

const userSchema = new mongoose.Schema({
  username: { type: String, required: true, unique: true },
  password: { type: String, required: true },
});

userSchema.pre('save', async function (next) {
  if (this.isModified('password') || this.isNew) {
    const salt = await bcrypt.genSalt(10);
    this.password = await bcrypt.hash(this.password, salt);
  }
  next();
});

const User = mongoose.model('User', userSchema);

module.exports = User;
```

### Step 5: Implement Registration and Login Routes

Create `auth.js` in the `routes` directory for handling authentication:

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');
const bcrypt = require('bcryptjs');
const User = require('../models/User');

const router = express.Router();
const secretKey = 'yourSecretKey'; // Store this in an environment variable

// Registration
router.post('/register', async (req, res) => {
  const { username, password } = req.body;
  try {
    let user = await User.findOne({ username });
    if (user) {
      return res.status(400).json({ msg: 'User already exists' });
    }

    user = new User({ username, password });
    await user.save();
    res.status(201).json({ msg: 'User registered successfully' });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Login
router.post('/login', async (req, res) => {
  const { username, password } = req.body;
  try {
    const user = await User.findOne({ username });
    if (!user) {
      return res.status(400).json({ msg: 'User does not exist' });
    }

    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) {
      return res.status(400).json({ msg: 'Invalid credentials' });
    }

    const payload = { userId: user._id };
    const token = jwt.sign(payload, secretKey, { expiresIn: '1h' });

    res.status(200).json({ token });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

module.exports = router;
```

### Step 6: Protect Routes with JWT Middleware

Create a middleware to protect routes that require authentication:

```javascript
const jwt = require('jsonwebtoken');
const secretKey = 'yourSecretKey'; // Use the same key from your environment variable

const auth = (req, res, next) => {
  const token = req.header('x-auth-token');
  if (!token) {
    return res.status(401).json({ msg: 'No token, authorization denied' });
  }

  try {
    const decoded = jwt.verify(token, secretKey);
    req.user = decoded.userId;
    next();
  } catch (err) {
    res.status(401).json({ msg: 'Token is not valid' });
  }
};

module.exports = auth;
```

### Step 7: Apply JWT Middleware to Protected Routes

Use the middleware to protect specific routes:

```javascript
const express = require('express');
const auth = require('./middleware/auth');

const router = express.Router();

// A protected route example
router.get('/protected', auth, (req, res) => {
  res.status(200).json({ msg: 'You have accessed a protected route', userId: req.user });
});

module.exports = router;
```

### Step 8: Integrate Front-End with JWT Authentication

In your React application, you can manage JWTs using `localStorage` or `sessionStorage` for storing tokens and `axios` for making authenticated requests.

**Example of a login function in React:**

```javascript
import axios from 'axios';

const login = async (username, password) => {
  try {
    const res = await axios.post('http://localhost:5000/auth/login', { username, password });
    const token = res.data.token;
    localStorage.setItem('token', token);
    // Redirect or perform further actions
  } catch (err) {
    console.error(err.response.data);
  }
};
```

**Example of setting up** `axios` to include JWT in headers:

```javascript
import axios from 'axios';

const api = axios.create({
  baseURL: 'http://localhost:5000',
});

api.interceptors.request.use(
  config => {
    const token = localStorage.getItem('token');
    if (token) {
      config.headers['x-auth-token'] = token;
    }
    return config;
  },
  error => {
    return Promise.reject(error);
  }
);

export default api;
```

### Conclusion

By following these steps, you should have a solid foundation for implementing JWT authentication in your MERN stack application. JWT provides a secure and scalable way to handle authentication, making it easier to protect your web application’s routes and resources.

Feel free to expand on this setup by adding features such as user roles, token refresh mechanisms, and enhanced security measures to further solidify your authentication process. Happy coding!