---
title: "Building Multi-Page Applications in React: A Router Tutorial"
seoTitle: "React Router: Building Multi-Page Apps"
seoDescription: "Learn how to build a multi-page application in React using React Router with this step-by-step tutorial"
datePublished: Sun Aug 11 2024 06:25:46 GMT+0000 (Coordinated Universal Time)
cuid: clzp6l51t00070alcdcn0fhin
slug: building-multi-page-applications-in-react-a-router-tutorial
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723357442083/5e617a2a-88f7-478a-8a87-7e4a58c0e215.png
tags: blogging, react-router, programming-blogs, css, js, programming, javascript, opensource, react, nodejs, reactjs, html5, general-advice, tailwind-css, reacthooks

---

Creating a multi-page application in React is straightforward with the help of React Router. React Router is a powerful library that allows you to implement routing in your React apps. In this article, we'll walk through the steps to set up a multi-page application using React Router, covering the basic concepts and code examples to get you started.

### What is React Router?

React Router is a library that enables dynamic routing in your React applications. It helps you manage navigation and render different components based on the URL path. With React Router, you can create a seamless multi-page experience within a single-page application.

### Getting Started

#### 1\. Install React Router

First, you need to install React Router. Open your terminal and run the following command:

```bash
npm install react-router-dom
```

#### 2\. Set Up Your Project Structure

Create a basic React project if you haven't already. Your project folder might look something like this:

```plaintext
my-app/
├── public/
├── src/
│   ├── components/
│   │   ├── Home.js
│   │   ├── About.js
│   │   └── Contact.js
│   ├── App.js
│   ├── index.js
│   └── App.css
└── package.json
```

#### 3\. Create Components for Each Page

Create the components for each page of your application. For this example, we'll create `Home.js`, `About.js`, and `Contact.js` in the `components` folder.

**Home.js**

```jsx
import React from 'react';

function Home() {
  return <h1>Home Page</h1>;
}

export default Home;
```

**About.js**

```jsx
import React from 'react';

function About() {
  return <h1>About Page</h1>;
}

export default About;
```

**Contact.js**

```jsx
import React from 'react';

function Contact() {
  return <h1>Contact Page</h1>;
}

export default Contact;
```

#### 4\. Set Up Routing in `App.js`

Now, configure routing in your `App.js` file. Import the necessary components from `react-router-dom` and set up your routes.

**App.js**

```jsx
import React from 'react';
import { BrowserRouter as Router, Route, Routes, Link } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Contact from './components/Contact';

function App() {
  return (
    <Router>
      <nav>
        <ul>
          <li><Link to="/">Home</Link></li>
          <li><Link to="/about">About</Link></li>
          <li><Link to="/contact">Contact</Link></li>
        </ul>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </Router>
  );
}

export default App;
```

In this code:

* `BrowserRouter` (aliased as `Router`) is used to handle the routing.
    
* `Route` defines the path and component to render.
    
* `Routes` wraps multiple `Route` components.
    
* `Link` is used to create navigation links.
    

#### 5\. Add Some Basic Styling

You can add some basic styles to your `App.css` to make the navigation look better.

**App.css**

```css
nav {
  background-color: #333;
  padding: 10px;
}

nav ul {
  list-style: none;
  padding: 0;
}

nav ul li {
  display: inline;
  margin-right: 10px;
}

nav ul li a {
  color: white;
  text-decoration: none;
}

nav ul li a:hover {
  text-decoration: underline;
}
```

#### 6\. Run Your App

Finally, run your React app with the following command:

```bash
npm start
```

Open your browser and navigate to [`http://localhost:3000`](http://localhost:3000). You should see your multi-page application with working navigation links.

### Conclusion

With React Router, building a multi-page app becomes a breeze. You’ve learned how to set up basic routing, create page components, and manage navigation. React Router’s flexibility and ease of use make it an essential tool for React developers, enabling you to build dynamic and user-friendly web applications.

---

## 💰 You can help me by Donating

[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black align="left")](https://buymeacoffee.com/dk119819)