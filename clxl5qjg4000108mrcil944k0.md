---
title: "Learn to Build a GitHub Repository Showcase Using HTML, CSS, and JavaScript"
seoTitle: "Build a GitHub Repository Showcase"
seoDescription: "Learn to build a dynamic GitHub repository showcase using HTML, CSS, and JavaScript for your personal portfolio"
datePublished: Wed Jun 19 2024 01:31:29 GMT+0000 (Coordinated Universal Time)
cuid: clxl5qjg4000108mrcil944k0
slug: learn-to-build-a-github-repository-showcase-using-html-css-and-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718760514208/272b206a-989b-4c83-8a8c-7d601edada00.png
tags: blogging, css3, css, js, github, javascript, html, nodejs, projects, git, reactjs, html5, project-management, github-actions-1, html-tags

---

Are you looking to create a personal portfolio that dynamically showcases your GitHub repositories? In this blog post, I'll guide you through building a web project using HTML, CSS, and JavaScript to display your repositories from GitHub. This is a fantastic way to demonstrate your work and technical skills to potential employers or collaborators.

### 1\. Setup Your Environment

Before starting, ensure you have a text editor (such as VSCode), a web browser, and a GitHub account.

1. **Text Editor:** Download and install [VSCode](https://code.visualstudio.com/).
    
2. **GitHub Account:** Ensure your repositories are public or use a GitHub token for private repositories.
    

### 2\. Create the Basic Structure

Let's start by setting up the basic file structure for our project.

**Project Structure:**

```bash
/github-repos
  |-- index.html
  |-- style.css
  |-- script.js
```

**index.html:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My GitHub Repositories</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>My GitHub Repositories</h1>
    </header>
    <main id="repo-container"></main>
    <script src="script.js"></script>
</body>
</html>
```

**style.css:**

```css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    color: #333;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
}

header {
    background: #333;
    color: #fff;
    padding: 10px 0;
    width: 100%;
    text-align: center;
}

#repo-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 20px;
}

.repo {
    background: #fff;
    margin: 10px;
    padding: 15px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
    width: 300px;
}

.repo h2 {
    margin: 0 0 10px;
    font-size: 1.5em;
}

.repo p {
    margin: 0 0 10px;
}
```

### 3\. Fetch GitHub Repositories

In the `script.js` file, we will fetch repositories from your GitHub account using the GitHub API.

**script.js:**

```js
document.addEventListener('DOMContentLoaded', function() {
    const username = 'your-github-username';
    const repoContainer = document.getElementById('repo-container');

    async function fetchRepositories() {
        try {
            const response = await fetch(`https://api.github.com/users/${username}/repos`);
            const repos = await response.json();
            displayRepositories(repos);
        } catch (error) {
            console.error('Error fetching repositories:', error);
        }
    }

    function displayRepositories(repos) {
        repos.forEach(repo => {
            const repoElement = document.createElement('div');
            repoElement.classList.add('repo');

            repoElement.innerHTML = `
                <h2>${repo.name}</h2>
                <p>${repo.description || 'No description available'}</p>
                <a href="${repo.html_url}" target="_blank">View Repository</a>
            `;

            repoContainer.appendChild(repoElement);
        });
    }

    fetchRepositories();
});
```

### 4\. Display Repositories Dynamically

The `displayRepositories` function dynamically creates HTML elements for each repository and appends them to the `repo-container` in the DOM. Each repository card includes the name, description, and a link to the repository.

### 5\. Style the Project

The provided CSS styles ensure that the project has a clean, responsive design. You can customize the styles further to match your personal branding.

### 6\. Deploy Your Project

Once your project is complete, you can deploy it using GitHub Pages for free. Here’s how:

1. **Create a Repository:** Create a new repository on GitHub and push your project files.
    
2. **Enable GitHub Pages:** Go to the repository settings, scroll down to the "GitHub Pages" section, and select the branch (e.g., `main`) and folder (e.g., `/root`) to deploy from.
    
3. **Access Your Site:** Your site will be available at `https://<your-username>.`[`github.io/<repository-name>/`](http://github.io/<repository-name>/).
    

### 7\. Conclusion

You've now created a dynamic web project to showcase your GitHub repositories using HTML, CSS, and JavaScript. This project not only highlights your technical skills but also serves as an interactive portfolio for potential employers and collaborators.

Feel free to expand on this project by adding more features such as filtering repositories by language, sorting by stars, or including your profile information. Happy coding!

---