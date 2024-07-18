---
title: "Firebase Authentication Made Simple: Detailed Code Examples"
seoTitle: "Simple Firebase Authentication: Code Examples"
seoDescription: "Learn how to implement Firebase Authentication with detailed code examples for email/password, social, and phone authentication methods"
datePublished: Thu Jun 20 2024 06:08:09 GMT+0000 (Coordinated Universal Time)
cuid: clxmv26te000e0ajs2q0egdvl
slug: firebase-authentication-made-simple-detailed-code-examples
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718863557025/255fb59c-8c12-4b64-8ac6-a469c4e7cfb2.png
tags: blogging, programming-blogs, css, js, programming, javascript, firebase, nodejs, projects, reactjs, html5, general-advice, 100daysofcode, firebaseauth, 100daysofprojects

---

[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black align="center")](https://buymeacoffee.com/dk119819)

## Introduction to Firebase Authentication

Firebase Authentication provides backend services to help authenticate users in your application. It supports various authentication methods, including email and password, phone numbers, and popular social media accounts like Google, Facebook, and Twitter. Firebase Authentication is easy to integrate, secure, and scalable, making it a popular choice for modern web and mobile applications.

In this guide, we will explore the various authentication methods provided by Firebase, including detailed step-by-step instructions and code snippets to help you implement these features in your application.

## Setting Up Firebase

### Creating a Firebase Project

1. **Go to the Firebase Console**: Open your browser and navigate to the [Firebase Console](https://console.firebase.google.com/).
    
2. **Create a New Project**: Click on the "Add Project" button. Provide a name for your project and follow the prompts to set it up. Enable Google Analytics if you need it for your project.
    

### Adding Firebase to Your Web App

1. **Register Your App**: In the Firebase Console, go to "Project Settings" and select "Add App". Choose the web app option and register your app by providing an App nickname.
    
2. **Install Firebase SDK**: Include Firebase in your web app by adding the Firebase SDK scripts to your HTML file. You can find the required scripts in the "Add Firebase to your web app" section of the setup wizard.
    
    ```html
    <!-- The core Firebase JS SDK is always required and must be listed first -->
    <script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-app.js"></script>
    
    <!-- Add Firebase products that you want to use -->
    <script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-auth.js"></script>
    ```
    
3. **Initialize Firebase**: Initialize Firebase in your application by adding the following code to your JavaScript file:
    
    ```javascript
    // Your web app's Firebase configuration
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT_ID.appspot.com",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID"
    };
    
    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);
    ```
    

## Firebase Authentication Methods

### Email and Password Authentication

Email and Password Authentication is one of the most commonly used authentication methods. It allows users to sign up and log in using their email addresses and passwords.

#### Setting Up Email/Password Authentication

1. **Enable the Authentication Method**: In the Firebase Console, navigate to the Authentication section and click on the "Sign-in method" tab. Enable the "Email/Password" sign-in method by toggling the switch.
    

#### User Registration

Create a simple HTML form for user registration:

```html
<form id="signup-form">
  <input type="email" id="signup-email" placeholder="Email" required>
  <input type="password" id="signup-password" placeholder="Password" required>
  <button type="submit">Sign Up</button>
</form>
```

Add the following JavaScript code to handle the form submission and register the user using Firebase Authentication:

```javascript
const signupForm = document.getElementById('signup-form');

signupForm.addEventListener('submit', (e) => {
  e.preventDefault();

  const email = document.getElementById('signup-email').value;
  const password = document.getElementById('signup-password').value;

  // Firebase function to create a new user with email and password
  firebase.auth().createUserWithEmailAndPassword(email, password)
    .then((userCredential) => {
      // Signed up successfully
      const user = userCredential.user;
      console.log('User registered:', user);
      // Redirect or display a message to the user
    })
    .catch((error) => {
      // Handle errors here
      const errorCode = error.code;
      const errorMessage = error.message;
      console.error('Error:', errorCode, errorMessage);
      // Display error message to the user
    });
});
```

#### User Login

Create a simple HTML form for user login:

```html
<form id="login-form">
  <input type="email" id="login-email" placeholder="Email" required>
  <input type="password" id="login-password" placeholder="Password" required>
  <button type="submit">Log In</button>
</form>
```

Add the following JavaScript code to handle the form submission and log in the user using Firebase Authentication:

```javascript
const loginForm = document.getElementById('login-form');

loginForm.addEventListener('submit', (e) => {
  e.preventDefault();

  const email = document.getElementById('login-email').value;
  const password = document.getElementById('login-password').value;

  // Firebase function to sign in a user with email and password
  firebase.auth().signInWithEmailAndPassword(email, password)
    .then((userCredential) => {
      // Signed in successfully
      const user = userCredential.user;
      console.log('User logged in:', user);
      // Redirect or display a message to the user
    })
    .catch((error) => {
      // Handle errors here
      const errorCode = error.code;
      const errorMessage = error.message;
      console.error('Error:', errorCode, errorMessage);
      // Display error message to the user
    });
});
```

#### Password Reset

Create a simple HTML form for password reset:

```html
<form id="reset-form">
  <input type="email" id="reset-email" placeholder="Email" required>
  <button type="submit">Reset Password</button>
</form>
```

Add the following JavaScript code to handle the form submission and send a password reset email using Firebase Authentication:

```javascript
const resetForm = document.getElementById('reset-form');

resetForm.addEventListener('submit', (e) => {
  e.preventDefault();

  const email = document.getElementById('reset-email').value;

  // Firebase function to send a password reset email
  firebase.auth().sendPasswordResetEmail(email)
    .then(() => {
      // Password reset email sent successfully
      console.log('Password reset email sent');
      // Display a message to the user
    })
    .catch((error) => {
      // Handle errors here
      const errorCode = error.code;
      const errorMessage = error.message;
      console.error('Error:', errorCode, errorMessage);
      // Display error message to the user
    });
});
```

### Social Authentication

Firebase supports authentication using various social providers like Google, Facebook, Twitter, and GitHub. Below, we'll walk through the steps for setting up Google Authentication as an example.

#### Setting Up Google Authentication

1. **Enable the Authentication Method**: In the Firebase Console, navigate to the Authentication section and click on the "Sign-in method" tab. Enable the "Google" sign-in method and provide the required credentials (Client ID and Client Secret).
    
2. **Add Google Sign-In Button**: Create a button in your HTML to trigger Google Sign-In:
    
    ```html
    <button id="google-signin">Sign in with Google</button>
    ```
    
3. **JavaScript for Handling Google Sign-In**: Add the following JavaScript code to handle the Google Sign-In process:
    
    ```javascript
    const googleSigninButton = document.getElementById('google-signin');
    
    googleSigninButton.addEventListener('click', () => {
      const provider = new firebase.auth.GoogleAuthProvider();
    
      firebase.auth().signInWithPopup(provider)
        .then((result) => {
          // Signed in successfully
          const user = result.user;
          console.log('User signed in with Google:', user);
          // Redirect or display a message to the user
        })
        .catch((error) => {
          // Handle errors here
          const errorCode = error.code;
          const errorMessage = error.message;
          console.error('Error:', errorCode, errorMessage);
          // Display error message to the user
        });
    });
    ```
    

### Phone Authentication

Phone authentication allows users to sign in using their phone number. Firebase sends a verification code to the user's phone number, which the user needs to enter to complete the sign-in process.

#### Setting Up Phone Authentication

1. **Enable the Authentication Method**: In the Firebase Console, navigate to the Authentication section and click on the "Sign-in method" tab. Enable the "Phone" sign-in method.
    
2. **HTML for Phone Authentication**: Create an HTML form to collect the user's phone number and verification code:
    
    ```html
    <form id="phone-auth-form">
      <input type="text" id="phone-number" placeholder="Phone Number" required>
      <button type="button" id="send-code">Send Verification Code</button>
      <input type="text" id="verification-code" placeholder="Verification Code" required>
      <button type="submit">Verify Code</button>
    </form>
    ```
    
3. **JavaScript for Sending Verification Code and Verifying Code**: Add the following JavaScript code to handle the phone authentication process:
    

```javascript
   const phoneAuthForm = document.getElementById('phone-auth-form');
   const sendCodeButton = document.getElementById('send-code');

   sendCode

Button.addEventListener('click', () => {
     const phoneNumber = document.getElementById('phone-number').value;
     const phoneProvider = new firebase.auth.PhoneAuthProvider();

     phoneProvider.verifyPhoneNumber(phoneNumber, /*recaptcha*/ null)
       .then((verificationId) => {
         const verificationCode = prompt('Enter the verification code sent to your phone');
         const credential = firebase.auth.PhoneAuthProvider.credential(verificationId, verificationCode);
         return firebase.auth().signInWithCredential(credential);
       })
       .then((result) => {
         // Phone authentication successful
         const user = result.user;
         console.log('User authenticated via phone:', user);
         // Redirect or display a message to the user
       })
       .catch((error) => {
         // Handle errors here
         const errorCode = error.code;
         const errorMessage = error.message;
         console.error('Error:', errorCode, errorMessage);
         // Display error message to the user
       });
   });
```

## Conclusion

Firebase Authentication offers a robust set of tools for implementing secure user authentication in your web and mobile applications. By following the steps outlined in this guide, you can integrate various authentication methods seamlessly into your project, ensuring a smooth user experience and enhanced security.

This guide covered the basics of setting up Firebase, implementing email/password authentication, social authentication with Google, and phone authentication. Firebase also supports additional features like anonymous authentication, custom authentication systems, and advanced security configurations, which you can explore further based on your application's requirements.

Implement Firebase Authentication today to streamline user management and enhance the security of your application!

---

This blog provides a comprehensive overview of Firebase Authentication, focusing on practical implementation steps and code examples to help developers integrate authentication features effectively. Happy Coding

## 💰 You can help me by Donating

[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black align="center")](https://buymeacoffee.com/dk119819)