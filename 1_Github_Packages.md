# Steps to Use GitHub Packages

## Why Use GitHub Packages?
GitHub Packages is a powerful package hosting service that integrates directly with your GitHub repositories. Here are some key reasons to use it:
- **Seamless Integration**: It works natively with GitHub, allowing you to store your code and packages in the same platform.
- **Centralized Management**: Host all your private and public dependencies in one place.
- **Security**: Keep your private packages secure by restricting access to authorized users or teams.
- **Version Control**: Easily manage and distribute different versions of your packages.
- **Automation**: Integrates with GitHub Actions to automate package publishing and CI/CD workflows.
- **Cost-Effective**: Avoid the need for third-party package hosting services if you’re already using GitHub.

By using GitHub Packages, you can maintain modular, reusable code and streamline updates across multiple projects.

## 1. Set Up Your Module Repository

### Create the Repository
- Create a new repository on GitHub for your module (e.g., `password-checker-module`).

### Initialize the Module Locally
```bash
mkdir password-checker-module
cd password-checker-module
git init
npm init -y
```

### Write Your Module Code
Create a file named `index.js`:
```javascript
// index.js
module.exports = function checkPasswordStrength(password) {
  const strongRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/;
  return strongRegex.test(password);
};
```

### Update `package.json`
Add the GitHub registry information:
```json
{
  "name": "@your-username/password-checker-module",
  "version": "1.0.0",
  "main": "index.js",
  "publishConfig": {
    "registry": "https://npm.pkg.github.com/"
  }
}
```

### Push to GitHub
```bash
git remote add origin https://github.com/your-username/password-checker-module.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

---

## 2. Authenticate with GitHub Packages

### Generate a Personal Access Token (PAT)
1. Go to **GitHub > Settings > Developer Settings > Personal Access Tokens**.
2. Click **Generate new token** and select:
   - `write:packages`
   - `read:packages`
   - `repo`
3. Copy the token.

### Authenticate with npm
Run the following command and use your GitHub username and PAT:
```bash
npm login --registry=https://npm.pkg.github.com
Username: your-username
Password: your-personal-access-token
Email: your-email@example.com
```

---

## 3. Publish the Module
Run the following command to publish your module to GitHub Packages:
```bash
npm publish
```

Your module is now hosted on GitHub Packages.

---

## 4. Use the Module in Another Project

### Install the Module
1. Add the GitHub Packages registry to your `.npmrc` file:
   ```bash
   echo "@your-username:registry=https://npm.pkg.github.com/" >> .npmrc
   ```

2. Install the module:
   ```bash
   npm install @your-username/password-checker-module
   ```

### Use the Module
Import and use it in your application:
```javascript
const checkPasswordStrength = require('@your-username/password-checker-module');

const password = "StrongP@ssw0rd";
if (checkPasswordStrength(password)) {
  console.log("Password is strong.");
} else {
  console.log("Password is weak.");
}
```

---

## 5. Update the Module

### Make Changes and Update Version
1. Modify your module code.
2. Update the version in `package.json` (e.g., `1.0.1`).

Run the following commands:
```bash
npm version patch
npm publish
```

### Update the Module in Your App
In the consuming project, update the module:
```bash
npm update @your-username/password-checker-module
```

---

## Advantages of GitHub Packages
- **Centralized Management**: All your private modules are hosted in one place.
- **Version Control**: GitHub handles versioning and distribution seamlessly.
- **Private and Secure**: Only users with repository access can install the package.
- **Integration with CI/CD**: Automate publishing with GitHub Actions.
