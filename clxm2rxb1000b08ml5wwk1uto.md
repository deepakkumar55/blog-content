---
title: "Step-by-Step Instructions for Task Management Apps"
seoTitle: "Task Management Apps: Step-by-Step Guide"
seoDescription: "Guide to building a task management app with MERN stack: user authentication, task CRUD, responsive UI, notifications, and collaboration"
datePublished: Wed Jun 19 2024 16:56:21 GMT+0000 (Coordinated Universal Time)
cuid: clxm2rxb1000b08ml5wwk1uto
slug: step-by-step-instructions-for-task-management-apps
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718816017534/6ae0095a-f9a8-4564-8e40-251072939c01.png
tags: express, blogging, programming-blogs, js, programming, javascript, opensource, nodejs, beginner, jwt, reactjs, beginners, general-advice, 100daysofcode, nodemailer

---

[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black align="center")](https://buymeacoffee.com/dk119819)

### Introduction

This guide provides a comprehensive step-by-step approach to developing a task management application using the MERN stack. The project includes user authentication, task CRUD operations, task categorization, a responsive and intuitive UI, notification features, and collaboration capabilities.

### Project Setup

#### Backend Setup

1. **Initialize the Project**
    
    ```bash
    mkdir task-manager
    cd task-manager
    npm init -y
    ```
    
2. **Install Dependencies**
    
    ```bash
    npm install express mongoose dotenv cors bcryptjs jsonwebtoken
    npm install --save-dev nodemon
    ```
    
3. **Project Structure**
    
    ```bash
    task-manager/
    ├── backend/
    │   ├── models/
    │   │   ├── Task.js
    │   │   └── User.js
    │   ├── routes/
    │   │   ├── auth.js
    │   │   └── tasks.js
    │   ├── middleware/
    │   │   └── auth.js
    │   ├── .env
    │   ├── server.js
    │   └── package.json
    ├── frontend/
    │   ├── public/
    │   ├── src/
    │   │   ├── components/
    │   │   ├── pages/
    │   |   |
    │   │   ├── App.js
    │   │   ├── index.js
    │   │   └── ... (other necessary files)
    │   ├── package.json
    │   └── ... (other necessary files)
    ├── package.json
    └── README.md
    ```
    

#### Frontend Setup

1. **Initialize React App**
    
    ```bash
    npx create-react-app frontend
    cd frontend
    ```
    
2. **Install Dependencies**
    
    ```bash
    npm install axios redux react-redux react-router-dom @mui/material @emotion/react @emotion/styled
    npm install @mui/icons-material
    ```
    
3. **Project Structure**
    
    ```bash
    frontend/
    ├── public/
    ├── src/
    │   ├── components/
    │   │   ├── Login.js
    │   │   ├── Registration.js
    │   │   ├── TaskForm.js
    │   │   ├── TaskList.js
    │   │   ├── ... (other necessary files)
    │   ├── pages/
    │   │   ├── HomePage.js
    │   │   └── ... (other necessary files)
    │   ├── App.js
    │   ├── index.js
    │   └── ... (other necessary files)
    ├── package.json
    └── ... (other necessary files)
    ```
    

### User Authentication

#### User Registration

1. **Backend: User Model (**`models/User.js`)
    
    ```javascript
    const mongoose = require('mongoose');
    
    const UserSchema = new mongoose.Schema({
        username: { type: String, required: true },
        email: { type: String, required: true, unique: true },
        password: { type: String, required: true }
    });
    
    module.exports = mongoose.model('User', UserSchema);
    ```
    
2. **Backend: Auth Routes (**`routes/auth.js`)
    
    ```javascript
    const express = require('express');
    const router = express.Router();
    const bcrypt = require('bcryptjs');
    const jwt = require('jsonwebtoken');
    const User = require('../models/User');
    
    router.post('/register', async (req, res) => {
        const { username, email, password } = req.body;
        try {
            let existingUser = await User.findOne({ email });
            if (existingUser) {
                return res.status(400).send('Email already registered');
            }
    
            const hashedPassword = await bcrypt.hash(password, 10);
            const newUser = new User({ username, email, password: hashedPassword });
            await newUser.save();
            res.status(201).send('User registered');
        } catch (error) {
            console.error('Registration error:', error);
            res.status(500).send('Server Error');
        }
    });
    
    module.exports = router;
    ```
    
3. **Frontend: Registration Component (**`components/Registration.js`)
    
    ```javascript
    import React, { useState } from 'react';
    import axios from 'axios';
    
    const Registration = () => {
        const [username, setUsername] = useState('');
        const [email, setEmail] = useState('');
        const [password, setPassword] = useState('');
        const [error, setError] = useState('');
    
        const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                const response = await axios.post('http://localhost:5000/api/auth/register', {
                    username,
                    email,
                    password
                });
                console.log(response.data);
                // Optionally handle success or redirect to login
            } catch (error) {
                setError('Registration failed. Please try again.');
            }
        };
    
        return (
            <div className="flex justify-center items-center h-screen">
                <form onSubmit={handleSubmit} className="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                    <h2 className="text-2xl mb-4">Register</h2>
                    <div className="mb-4">
                        <input type="text" value={username} onChange={(e) => setUsername(e.target.value)} className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" placeholder="Username" required />
                    </div>
                    <div className="mb-4">
                        <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" placeholder="Email" required />
                    </div>
                    <div className="mb-4">
                        <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" placeholder="Password" required />
                    </div>
                    {error && <p className="text-red-500 text-xs italic">{error}</p>}
                    <button type="submit" className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                        Register
                    </button>
                </form>
            </div>
        );
    };
    
    export default Registration;
    ```
    

#### User Login

1. **Backend: Auth Routes (**`routes/auth.js`)
    
    ```javascript
    router.post('/login', async (req, res) => {
        const { email, password } = req.body;
    
        try {
            const user = await User.findOne({ email });
            if (!user) {
                return res.status(401).json({ msg: 'Invalid credentials' });
            }
    
            const isMatch = await bcrypt.compare(password, user.password);
            if (!isMatch) {
                return res.status(401).json({ msg: 'Invalid credentials' });
            }
    
            const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET, { expiresIn: '1h' });
            res.json({ token });
        } catch (err) {
            console.error(err.message);
            res.status(500).send('Server Error');
        }
    });
    ```
    
2. **Frontend: Login Component (**`components/Login.js`)
    
    ```javascript
    import React, { useState } from 'react';
    import axios from 'axios';
    import { Link } from 'react-router-dom';
    
    const Login = ({ onLogin }) => {
        const [email, setEmail] = useState('');
        const [password, setPassword] = useState('');
        const [error, setError] = useState('');
    
        const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                const response = await axios.post('http://localhost:5000/api/auth/login', { email, password });
                const token = response.data.token;
                onLogin(token); // Notify parent component (App.js) about successful login
            } catch (error) {
                if (error.response) {
                    setError('Invalid credentials. Please try again.');
                } else {
                    setError('Something went wrong. Please try again later.');
                }
            }
        };
    
        return (
            <div className="flex justify-center items-center h-screen">
                <form onSubmit={handleSubmit} className="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                    <h2 className="text-2xl mb-4">Login</h2>
                    <div className="mb-4">
                        <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" placeholder="Email" required />
                    </div>
                    <div className="mb-4">
                        <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" placeholder="Password" required />
                    </div>
                    {error && <p className="text-red-500 text-xs italic">{error}</p>}
                    <button type="submit" className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                        Login
                    </button>
                    <p className="mt-4">
                        Don't have an account? <Link to="/register" className="text-blue-500 hover:text-blue-700">Register here</Link>
                    </p>
                </form>
            </div>
        );
    };
    
    export default Login;
    ```
    

#### JWT Authentication

1. **Backend: Auth Middleware (**`middleware/auth.js`)
    
    ```javascript
    const jwt = require('jsonwebtoken');
    
    const authMiddleware = (req, res, next) => {
        const token = req.header('Authorization')?.replace('Bearer ', '');
        if (!token) {
            return res.status(401).send('Access denied');
        }
    
        try {
            const verified = jwt.verify(token, process.env.JWT_SECRET);
            req.user = verified;
            next();
        } catch (error) {
            res.status(400).send('Invalid token');
        }
    };
    
    module.exports = authMiddleware;
    ```
    
2. **Backend: Protecting Routes**
    
    ```javascript
    const express = require('express');
    const router = express.Router();
    const Task = require('../models/Task');
    const authMiddleware = require('../middleware/auth');
    
    // Example of a protected route
    router.get('/', authMiddleware, async (req, res) => {
        try {
            const tasks = await Task.find({ userId: req.user.userId });
            res.json(tasks);
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    
    // ... other routes
    ```
    

### Task CRUD Operations

#### Create Task

1. **Backend: Task Model (**`models/Task.js`)
    
    ```javascript
    const mongoose = require('mongoose');
    
    const TaskSchema = new mongoose.Schema({
        title: { type: String, required: true },
        description: { type: String, required: true },
        status: { type: String, default: 'pending' },
        dueDate: { type: Date },
        category: { type: String },
        userId: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true }
    });
    
    module.exports = mongoose.model('Task', TaskSchema);
    ```
    
2. **Backend: Task Routes (**`routes/tasks.js`)
    
    ```javascript
    const express = require('express');
    const router = express.Router();
    const Task = require('../models/Task');
    const authMiddleware = require('../middleware/auth');
    
    router.post('/', authMiddleware, async (req, res) => {
        const { title, description, status, dueDate, category } = req.body;
        const task = new Task({ title, description, status, dueDate, category, userId: req.user.userId });
        try {
            await task.save();
            res.status(201).json(task);
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    
    // ... other routes
    ```
    
3. **Frontend: TaskForm Component (**`components/TaskForm.js`)
    
    ```javascript
    import React, { useState } from 'react';
    import axios from 'axios';
    
    const TaskForm = ({ token }) => {
        const [title, setTitle] = useState('');
        const [description, setDescription] = useState('');
        const [status, setStatus] = useState('pending');
        const [dueDate, setDueDate] = useState('');
        const [category, setCategory] = useState('');
        const [error, setError] = useState('');
    
        const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                await axios.post('http://localhost:5000/api/tasks', {
                    title,
                    description,
                    status,
                    dueDate,
                    category
                }, {
                    headers: {
                        Authorization: `Bearer ${token}`
                    }
                });
                setTitle('');
                setDescription('');
                setStatus('pending');
                setDueDate('');
                setCategory('');
                setError('');
            } catch (error) {
                setError('Error adding task. Please try again.');
            }
        };
    
        return (
            <div className="container mx-auto">
                <h2 className="text-2xl font-bold mb-4">Add New Task</h2>
                <form onSubmit={handleSubmit} className="mb-8">
                    <div className="flex mb-4">
                        <input type="text" value={title} onChange={(e) => setTitle(e.target.value)} className="shadow appearance-none border rounded w-1/2 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mr-2" placeholder="Title" required />
                        <input type="text" value={description} onChange={(e) => setDescription(e.target.value)} className="shadow appearance-none border rounded w-1/2 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline ml-2" placeholder="Description" required />
                    </div>
                    <div className="flex mb-4">
                        <input type="text" value={dueDate} onChange={(e) => setDueDate(e.target.value)} className="shadow appearance-none border rounded w-1/2 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mr-2" placeholder="Due Date (Optional)" />
                        <input type="text" value={category} onChange={(e) => setCategory(e.target.value)} className="shadow appearance-none border rounded w-1/2 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline ml-2" placeholder="Category (Optional)" />
                    </div>
                    <div className="mb-4">
                        <select value={status} onChange={(e) => setStatus(e.target.value)} className="shadow appearance-none border rounded w-1/4 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                            <option value="pending">Pending</option>
                            <option value="in_progress">In Progress</option>
                            <option value="completed">Completed</option>
                        </select>
                    </div>
                    <button type="submit" className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                        Add Task
                    </button>
                </form>
                {error && <p className="text-red-500 text-xs italic">{error}</p>}
            </div>
        );
    };
    
    export default TaskForm;
    ```
    

#### Read Tasks

1. **Backend: Task Routes (**`routes/tasks.js`)
    
    ```javascript
    router.get('/', authMiddleware, async (req, res) => {
        try {
            const tasks = await Task.find({ userId: req.user.userId });
            res.json(tasks);
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    ```
    
2. **Frontend: TaskList Component (**`components/TaskList.js`)
    
    ```javascript
    import React, { useState, useEffect } from 'react';
    import axios from 'axios';
    
    const TaskList = ({ token }) => {
        const [tasks, setTasks] = useState([]);
        const [error, setError] = useState('');
    
        useEffect(() => {
            const fetchTasks = async () => {
                try {
                    const response = await axios.get('http://localhost:5000/api/tasks', {
                        headers: {
                            Authorization: `Bearer ${token}`
                        }
                    });
                    setTasks(response.data);
                } catch (error) {
                    setError('Error fetching tasks. Please try again.');
                }
            };
            fetchTasks();
        }, [token]);
    
        const handleDelete = async (id) => {
            try {
                await axios.delete(`http://localhost:5000/api/tasks/${id}`, {
                    headers: {
                        Authorization: `Bearer ${token}`
                    }
                });
                setTasks(tasks.filter(task => task._id !== id));
            } catch (error) {
                setError('Error deleting task. Please try again.');
            }
        };
    
        return (
            <div className="container mx-auto">
                <h2 className="text-2xl font-bold mb-4">Task List</h2>
                {error && <p className="text-red-500 text-xs italic">{error}</p>}
                {tasks.map(task => (
                    <div key={task._id} className="mb-4 p-4 border rounded shadow">
                        <h3 className="font-bold">{task.title}</h3>
                        <p>{task.description}</p>
                        <p><strong>Status:</strong> {task.status}</p>
                        {task.dueDate && <p><strong>Due Date:</strong> {task.dueDate}</p>}
                        {task.category && <p><strong>Category:</strong> {task.category}</p>}
                        <button onClick={() => handleDelete(task._id)} className="mt-2 bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                            Delete
                        </button>
                    </div>
                ))}
            </div>
        );
    };
    
    export default TaskList;
    ```
    

#### Update Task

1. **Backend: Task Routes (**`routes/tasks.js`)
    
    ```javascript
    router.put('/:id', authMiddleware, async (req, res) => {
        const { title, description, status, dueDate, category } = req.body;
        try {
            const updatedTask = await Task.findByIdAndUpdate(req.params.id, { title, description, status, dueDate, category }, { new: true });
            res.json(updatedTask);
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    ```
    
2. **Frontend: TaskManager Component with Edit Capability (**`components/TaskManager.js`)
    
    ```javascript
    import React, { useState, useEffect } from 'react';
    import axios from 'axios';
    
    const TaskManager = ({ token }) => {
        const [tasks, setTasks] = useState([]);
        const [title, setTitle] = useState('');
        const [description, setDescription] = useState('');
        const [status, setStatus] = useState('pending');
        const [dueDate, setDueDate] = useState('');
        const [category, setCategory] = useState('');
        const [editingTask, setEditingTask] = useState(null);
        const [error, setError] = useState('');
    
        useEffect(() => {
            const fetchTasks = async () => {
                try {
                    const response = await axios.get('http://localhost:5000/api/tasks', {
                        headers: {
                            Authorization: `Bearer ${token}`
                        }
                    });
                    setTasks(response.data);
                } catch (error) {
                    setError('Error fetching tasks. Please try again.');
                }
            };
            fetchTasks();
        }, [token]);
    
        const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                if (editingTask) {
                    const response = await axios.put(`http://localhost:5000/api/tasks/${editingTask._id}`, {
                        title,
                        description,
                        status,
                        dueDate,
                        category
                    }, {
                        headers: {
                            Authorization: `Bearer ${token}`
                        }
                    });
                    setTasks(tasks.map(task => (task._id === editingTask._id ? response.data : task)));
                } else {
                    const response = await axios.post('http://localhost:5000/api/tasks', {
                        title,
                        description,
                        status,
                        dueDate,
                        category
                    }, {
                        headers: {
                            Authorization: `Bearer ${token}`
                        }
                    });
                    setTasks([...tasks, response.data]);
                }
                resetForm();
            } catch (error) {
                setError('Task submission failed. Please try again.');
            }
        };
    
        const resetForm = () => {
            setTitle('');
            setDescription('');
            setStatus('pending');
            setDueDate('');
            setCategory('');
            setEditingTask(null);
        };
    
        const handleEdit = (task) => {
            setTitle(task.title);
            setDescription(task.description);
            setStatus(task.status);
            setDueDate(task.dueDate ? task.dueDate.substring(0, 10) : '');
            setCategory(task.category);
            setEditingTask(task);
        };
    
        const handleDelete = async (id) => {
            try {
                await axios.delete(`http://localhost:5000/api/tasks/${id}`, {
                    headers: {
                        Authorization: `Bearer ${token}`
                    }
                });
                setTasks(tasks.filter(task => task._id !== id));
            } catch (error) {
                setError('Error deleting task. Please try again.');
            }
        };
    
        return (
            <div className="container mx-auto">
                <h2 className="text-2xl font-bold mb-4">Task Manager</h2>
                <form onSubmit={handleSubmit} className="mb-8">
                    <div className="flex mb-4">
                        <input type="text" value={title} onChange={(e) => setTitle(e.target.value)} className="shadow appearance-none border rounded w-1/2 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mr-2" placeholder="Title" required />
                        <input type="text" value={description} onChange={(e) => setDescription(e.target.value)} className="shadow appearance-none border rounded w-1/2 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline ml-2" placeholder="Description" required />
                    </div>
                    <div className="flex mb-4">
                        <input type="text" value={dueDate} onChange={(e) => setDueDate(e.target.value)} className="shadow appearance-none border rounded w-1/2 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline mr-2" placeholder="Due Date (Optional)" />
                        <input type="text" value={category} onChange={(e) => setCategory(e.target.value)} className="shadow appearance-none border rounded w-1/2 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline ml-2" placeholder="Category (Optional)" />
                    </div>
                    <div className="mb-4">
                        <select value={status} onChange={(e) => setStatus(e.target.value)} className="shadow appearance-none border rounded w-1/4 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                            <option value="pending">Pending</option>
                            <option value="in_progress">In Progress</option>
                            <option value="completed">Completed</option>
                        </select>
                    </div>
                    <button type="submit" className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                        {editingTask ? 'Update Task' : 'Add Task'}
                    </button>
                </form>
                {error && <p className="text-red-500 text-xs italic">{error}</p>}
                <div>
                    {tasks.map(task => (
                        <div key={task._id} className="mb-4 p-4 border rounded shadow">
                            <h3 className="font-bold">{task.title}</h3>
                            <p>{task.description}</p>
                            <p><strong>Status:</strong> {task.status}</p>
                            {task.dueDate && <p><strong>Due Date:</strong> {task.dueDate}</p>}
                            {task.category && <p><strong>Category:</strong> {task.category}</p>}
                            <button onClick={() => handleEdit(task)} className="mt-2 bg-yellow-500 hover:bg-yellow-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline mr-2">
                                Edit
                            </button>
                            <button onClick={() => handleDelete(task._id)} className="mt-2 bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                                Delete
                            </button>
                        </div>
                    ))}
                </div>
            </div>
        );
    };
    
    export default TaskManager;
    ```
    

#### Delete Task

1. **Backend: Task Routes (**`routes/tasks.js`)
    
    ```javascript
    router.delete('/:id', authMiddleware, async (req, res) => {
        try {
            await Task.findByIdAndDelete(req.params.id);
            res.status(204).send();
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    ```
    

### Task Categories

#### Add Task to Categories

This feature is already covered in the Task CRUD operations where we have the `category` field in the task model and forms.

#### Filter Tasks by Category

1. **Backend: Task Routes (**`routes/tasks.js`)
    
    ```javascript
    router.get('/category/:category', authMiddleware, async (req, res) => {
        try {
            const tasks = await Task.find({ userId: req.user.userId, category: req.params.category });
            res.json(tasks);
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    ```
    
2. **Frontend: TaskList Component (**`components/TaskList.js`)
    
    ```javascript
    import React, { useState, useEffect } from 'react';
    import axios from 'axios';
    
    const TaskList = ({ token }) => {
        const [tasks, setTasks] = useState([]);
        const [category, setCategory] = useState('');
        const [error, setError] = useState('');
    
        useEffect(() => {
            const fetchTasks = async () => {
                try {
                    const response = await axios.get('http://localhost:5000/api/tasks', {
                        headers: {
                            Authorization: `Bearer ${token}`
                        }
                    });
                    setTasks(response.data);
                } catch (error) {
                    setError('Error fetching tasks. Please try again.');
                }
            };
            fetchTasks();
        }, [token]);
    
        const handleCategoryChange = async (e) => {
            setCategory(e.target.value);
            try {
                const response = await axios.get(`http://localhost:5000/api/tasks/category/${e.target.value}`, {
                    headers: {
                        Authorization: `Bearer ${token}`
                    }
                });
                setTasks(response.data);
            } catch (error) {
                setError('Error fetching tasks by category. Please try again.');
            }
        };
    
        return (
            <div className="container mx-auto">
                <h2 className="text-2xl font-bold mb-4">Task List</h2>
                <select value={category} onChange={handleCategoryChange} className="mb-4 shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                    <option value="">All Categories</option>
                    <option value="Work">Work</option>
                    <option value="Personal">Personal</option>
                    {/* Add more categories as needed */}
                </select>
                {error && <p className="text-red-500 text-xs italic">{error}</p>}
                {tasks.map(task => (
                    <div key={task._id} className="mb-4 p-4 border rounded shadow">
                        <h3 className="font-bold">{task.title}</h3>
                        <p>{task.description}</p>
                        <p><strong>Status:</strong> {task.status}</p>
                        {task.dueDate && <p><strong>Due Date:</strong> {task.dueDate}</p>}
                        {task.category && <p><strong>Category:</strong> {task.category}</p>}
                        <button onClick={() => handleDelete(task._id)} className="mt-2 bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                            Delete
                        </button>
                    </div>
                ))}
            </div>
        );
    };
    
    export default TaskList;
    ```
    

### UI/UX Design

#### Responsive Design

1. **Using Tailwind CSS**
    
    * Install Tailwind CSS:
        
        ```bash
        npm install tailwindcss
        npx tailwindcss init
        ```
        
    * Configure `tailwind.config.js`:
        
        ```javascript
        module.exports = {
          content: [
            "./src/**/*.{js,jsx,ts,tsx}",
          ],
          theme: {
            extend: {},
          },
          plugins: [],
        }
        ```
        
    * Import Tailwind CSS in `index.css`:
        
        ```css
        @tailwind base;
        @tailwind components;
        @tailwind utilities;
        ```
        

#### User-Friendly Interface

Utilize Material-UI components for a more polished look and feel. For example, use `TextField`, `Button`, and other components from Material-UI to create forms and buttons.

#### Drag-and-Drop Functionality

1. **Install React DnD**
    
    ```bash
    npm install react-dnd react-dnd-html5-backend
    ```
    
2. **Implement Drag-and-Drop in TaskList Component**
    
    ```javascript
    import React, { useState, useEffect } from 'react';
    import axios from 'axios';
    import { useDrag, useDrop } from 'react-dnd';
    import { HTML5Backend } from 'react-dnd-html5-backend';
    import { DndProvider } from 'react-dnd';
    
    const ItemType = {
        TASK: 'task'
    };
    
    const Task = ({ task, index, moveTask }) => {
        const [, ref] = useDrag({
            type: ItemType.TASK,
            item: { index },
        });
    
        const [, drop] = useDrop({
            accept: ItemType.TASK,
            hover: (item) => {
                if (item.index !== index) {
                    moveTask(item.index, index);
                    item.index = index;
                }
            },
        });
    
        return (
            <div ref={(node) => ref(drop(node))} className="mb-4 p-4 border rounded shadow">
                <h3 className="font-bold">{task.title}</h3>
                <p>{task.description}</p>
                <p><strong>Status:</strong> {task.status}</p>
                {task.dueDate && <p><strong>Due Date:</strong> {task.dueDate}</p>}
                {task.category && <p><strong>Category:</strong> {task.category}</p>}
            </div>
        );
    };
    
    const TaskList = ({ token }) => {
        const [tasks, setTasks] = useState([]);
        const [error, setError] = useState('');
    
        useEffect(() => {
            const fetchTasks = async () => {
                try {
                    const response = await axios.get('http://localhost:5000/api/tasks', {
                        headers: {
                            Authorization: `Bearer ${token}`
                        }
                    });
                    setTasks(response.data);
                } catch (error) {
                    setError('Error fetching tasks. Please try again.');
                }
            };
            fetchTasks();
        }, [token]);
    
        const moveTask = (fromIndex, toIndex) => {
            const updatedTasks = [...tasks];
            const [movedTask] = updatedTasks.splice(fromIndex, 1);
            updatedTasks.splice(toIndex, 0, movedTask);
            setTasks(updatedTasks);
        };
    
        return (
            <DndProvider backend={HTML5Backend}>
                <div className="container mx-auto">
                    <h2 className="text-2xl font-bold mb-4">Task List</h2>
                    {error && <p className="text-red-500 text-xs italic">{error}</p>}
                    {tasks.map((task, index) => (
                        <Task key={task._id} index={index} task={task} moveTask={moveTask} />
                    ))}
                </div>
            </DndProvider>
        );
    };
    
    export default TaskList;
    ```
    

### Notifications

#### Email Notifications

1. **Install Nodemailer**
    
    ```bash
    npm install nodemailer
    ```
    
2. **Configure Nodemailer in Backend**
    
    ```javascript
    const nodemailer = require('nodemailer');
    
    const transporter = nodemailer.createTransport({
        service: 'gmail',
        auth: {
            user: process.env.EMAIL,
            pass: process.env.EMAIL_PASSWORD
        }
    });
    
    const sendNotification = (email, subject, text) => {
        const mailOptions = {
            from: process.env.EMAIL,
            to: email,
            subject: subject,
            text: text
        };
    
        transporter.sendMail(mailOptions, (error, info) => {
            if (error) {
                console.error('Error sending email:', error);
            } else {
                console.log('Email sent:', info.response);
            }
        });
    };
    
    module.exports = sendNotification;
    ```
    
3. **Send Notification on Task Due Date**
    
    ```javascript
    const sendNotification = require('../utils/sendNotification');
    
    router.post('/', authMiddleware, async (req, res) => {
        const { title, description, status, dueDate, category } = req.body;
        const task = new Task({ title, description, status, dueDate, category, userId: req.user.userId });
        try {
            await task.save();
            sendNotification(req.user.email, 'New Task Created', `You have a new task: ${title}`);
            res.status(201).json(task);
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    ```
    

#### In-App Notifications

1. **Install** [**Socket.io**](http://Socket.io)
    
    ```bash
    npm install socket.io
    ```
    
2. **Configure** [**Socket.io**](http://Socket.io) **in Backend**
    
    ```javascript
    const http = require('http');
    const socketio = require('socket.io');
    
    const server = http.createServer(app);
    const io = socketio(server);
    
    io.on('connection', (socket) => {
        console.log('New WebSocket connection');
    
        socket.on('disconnect', () => {
            console.log('WebSocket disconnected');
        });
    });
    
    // Change app.listen to server.listen
    server.listen(PORT, () => console.log(`Server running on http://localhost:${PORT}`));
    ```
    
3. **Frontend: Configure** [**Socket.io**](http://Socket.io) **Client**
    
    ```javascript
    import React, { useEffect } from 'react';
    import io from 'socket.io-client';
    
    const socket = io('http://localhost:5000');
    
    const Notifications = () => {
        useEffect(() => {
            socket.on('notification', (message) => {
                alert(message);
            });
        }, []);
    
        return <div>Notifications Component</div>;
    };
    
    export default Notifications;
    ```
    

### Collaboration

#### Share Tasks

1. **Backend: Add Shared Users to Task Model**
    
    ```javascript
    const TaskSchema = new mongoose.Schema({
        // ... other fields
        sharedWith: [{ type: mongoose.Schema.Types.ObjectId, ref: 'User' }]
    });
    ```
    
2. **Backend: Share Task Route**
    
    ```javascript
    router.post('/:id/share', authMiddleware, async (req, res) => {
        const { userId } = req.body;
        try {
            const task = await Task.findById(req.params.id);
            if (!task) {
                return res.status(404).send('Task not found');
            }
            task.sharedWith.push(userId);
            await task.save();
            res.status(200).json(task);
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    ```
    
3. **Frontend: Share Task Form**
    
    ```javascript
    import React, { useState } from 'react';
    import axios from 'axios';
    
    const ShareTaskForm = ({ taskId, token }) => {
        const [email, setEmail] = useState('');
        const [error, setError] = useState('');
    
        const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                const response = await axios.post(`http://localhost:5000/api/tasks/${taskId}/share`, { email }, {
                    headers: {
                        Authorization: `Bearer ${token}`
                    }
                });
                setEmail('');
                setError('');
            } catch (error) {
                setError('Error sharing task. Please try again.');
            }
        };
    
        return (
            <form onSubmit={handleSubmit}>
                <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} placeholder="User Email" required />
                <button type="submit">Share Task</button>
                {error && <p>{error}</p>}
            </form>
        );
    };
    
    export default ShareTaskForm;
    ```
    

#### Assign Tasks

1. **Backend: Add Assigned User to Task Model**
    
    ```javascript
    const TaskSchema = new mongoose.Schema({
        // ... other fields
        assignedTo: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
    });
    ```
    
2. **Backend: Assign Task Route**
    
    ```javascript
    router.post('/:id/assign', authMiddleware, async (req, res) => {
        const { userId } = req.body;
        try {
            const task = await Task.findById(req.params.id);
            if (!task) {
                return res.status(404).send('Task not found');
            }
            task.assignedTo = userId;
            await task.save();
            res.status(200).json(task);
        } catch (error) {
            res.status(500).send('Server Error');
        }
    });
    ```
    
3. **Frontend: Assign Task Form**
    
    ```javascript
    import React, { useState } from 'react';
    import axios from 'axios';
    
    const AssignTaskForm = ({ taskId, token }) => {
        const [email, setEmail] = useState('');
        const [error, setError] = useState('');
    
        const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                const response = await axios.post(`http://localhost:5000/api/tasks/${taskId}/assign`, { email }, {
                    headers: {
                        Authorization: `Bearer ${token}`
                    }
                });
                setEmail('');
                setError('');
            } catch (error) {
                setError('Error assigning task. Please try again.');
            }
        };
    
        return (
            <form onSubmit={handleSubmit}>
                <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} placeholder="User Email" required />
                <button type="submit">Assign Task</button>
                {error && <p>{error}</p>}
            </form>
        );
    };
    
    export default AssignTaskForm;
    ```
    

### Complete Code Integration

Combine all components and features into a cohesive project.

#### Backend (`server.js`)

```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();
const http = require('http');
const socketio = require('socket.io');

const authRoutes = require('./routes/auth');
const taskRoutes = require('./routes/tasks');

const app = express();
const server = http.createServer(app);
const io = socketio(server);

app.use(cors());
app.use(express.json());

mongoose.connect(process.env.MONGODB_URI, {
    useNewUrlParser: true,
    useUnifiedTopology: true,
}).then(() => console.log('MongoDB connected'))
  .catch(err => console.error('MongoDB connection error:', err));

app.use('/api/auth', authRoutes);
app.use('/api/tasks', taskRoutes);

io.on('connection', (socket) => {
    console.log('New WebSocket connection');
    socket.on('disconnect', () => {
        console.log('WebSocket disconnected');
    });
});

const PORT = process.env.PORT || 5000;
server.listen(PORT, () => console.log(`Server running on http://localhost:${PORT}`));
```

#### Frontend (`App.js`)

```javascript
import React, { useState } from 'react';
import { BrowserRouter as Router, Routes, Route, Navigate } from 'react-router-dom';
import Login from './components/Login';
import Registration from './components/Registration';
import TaskManager from './components/TaskManager';
import Notifications from './components/Notifications';

const App = () => {
    const [token, setToken] = useState('');

    const handleLogin = (token) => {
        setToken(token);
    };

    const handleLogout = () => {
        setToken('');
    };

    return (
        <Router>
            <div className="App">
                <Routes>
                    <Route path="/login" element={<Login onLogin={handleLogin} />} />
                    <Route path="/register" element={<Registration />} />
                    <Route
                        path="/tasks"
                        element={
                            token ? (
                                <>
                                    <button onClick={handleLogout} className="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
                                        Logout
                                    </button>
                                    <TaskManager token={token} />
                                    <Notifications />
                                </>
                            ) : (
                                <Navigate to="/login" />
                            )
                        }
                    />
                    <Route path="/" element={<Navigate to="/login" />} />
                </Routes>
            </div>
        </Router>
    );
};

export default App;
```

### Final Thoughts

This guide provides a comprehensive overview of developing a task management application using the MERN stack. By following these steps, you can create a fully functional application with user authentication, task management, responsive design, notifications, and collaboration features.

Keep exploring and enhancing your application by adding more features and improving the existing ones. Happy coding!

## 💰 You can help me by Donating

[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black align="center")](https://buymeacoffee.com/dk119819)