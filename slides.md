---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /assets/intro.jpg
# some information about your slides (markdown enabled)
title: Software Development | Foundations
info: |
  ## Software Development | Foundations
# apply unocss classes to the current slide
class: text-left
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Intro to Deployment
Unit 07 - Lesson 06

- [ ] Practice creating Pull Requests (PRs) on Github
- [ ] Github Actions
- [ ] Continuous Integration/Continuous Deployment (CI/CD)

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
-->

---
transition: slide-left
---

# To install for Next Class

- Install Expo Go
- if on Mac, may need to install XCode

## Ranks in Web Dev

- Junior: 0-2 years
- Intermediate: 2-4 years
- Intermediate II: 3-5 years
- Senior: 5-8 years
- Tech Lead: 8+ years
- Manager: Can you balance needs of Developers vs Product/Senior leadership?
- Staff: How well can you communicate/get along/push back with senior leadership?  
- Director
- VP

---
transition: slide-left
---

# Steps to Force PRs on GH Repo

1. Goto your Github repo
2. Click Settings tab in top-right corner
3. Left menu click Branches
4. click "Add classic branch protection rule"
5. in Branch name pattern, type: `main` (for the branch name you want to protect)
6. Check the following options:
  - require a pull request before merging / require approvals
  - require status checks to pass before merging 
  - lock branch
  - click Create button at bottom
- Collaborators are forced to create PRs which can be code-reviewed and approved before merging.  They can push to feature branches, but not push or merge directly to main.

---
transition: slide-left
---

# Practice the PR process

- Clone https://github.com/avcoder/ts-exercise-01
- I'll invite you as a collaborator
- Make a change in the codebase
- Try to push (you shouldn't be able to)
- Create a PR
- Someone else can code review it and eventually approve it after back/forth convo
- (Try to merge PR if possible)
- Otherwise I'll merge it

---
transition: slide-left
---

# What is CI/CD?
Aims to improve speed, efficiency, and reliability of software delivery

-  merge your code changes into the shared repository without breaking anything
- Continuous Integration:
  - Changes are committed regularly; Unit tests are run
  - Goal: identify problems early
- Continuous Delivery:
  - Automated build processes to prepare for release after testing
  - Goal: always have a version of software that can be deployed
- Continuous Deployment:
  - Fully automated deployment to prod environments

---
transition: slide-left
---

# CI/CD Phases

- Build phase: upon pushing code, that event triggers an automatic `npm run build` where code is compiled into a single executable (see Netlify's terminal during build)
- Test phase: The build is tested to ensure no errors in Unit Tests, Linting, Typescript, etc.
- Staging: The app is run in a production-like environment (ex: a temporary url) that devs can test to ensure it's ready for prod
- Deployment: App is automatically deployed to end-users

<img src="/assets/cicd2.webp" style="height: 250px" >

---
transition: slide-left
---

# Tools for CI/CD

- There are several tools available for implementing CI/CD pipelines:
  - Jenkins, Travis CI, Github Actions, Built-in CI/CD features by hosts like Netlify/Vercel

<img src="/assets/cicd4.jpg" style="height: 300px">

---
transition: slide-left
---

# Github Actions

- **Events** is when something happens (new push, PR, new issue etc) that triggers to run a workflow
- **Runners** are servers that runs your tasks 
- **Jobs** is a collection of steps (simple commands, scripts, actions) executed on the same runner and are defined in a workflow.  
- **Workflows** is a series of jobs triggered upon an event; coded in yaml; stored .github/workflows/ in your repo
- **Github Actions** consist of events, jobs, tasks, runners, workflows.

<img src="/assets/cicd3.webp" style="height: 230px">
---
transition: slide-left
---

# Starter Workflow

- `on:` - defines triggers on certain branches to run workflow (like JS add event listeners) 
- `permissions:` - made available to Actions/Commands that provide GH token to access GH API
- `jobs:` - sets up job and runner to process work flow and steps to run it

```yaml
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

permissions:
  contents: read    # Allows checkout and read-only access to the repo content
  pull-requests: read  # Required if your workflow interacts with PR metadata (e.g., checks)

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repository
      uses: actions/checkout@v4

    - name: Run tests
      run: npm test

```

---
transition: slide-left
---

# Steps
Most of work takes place in Steps

```yaml
    steps:
    - name: Checkout repository
      uses: actions/checkout@v4 # 1st step: checks out the code from branch

    - name: Use Node.js 
      uses: actions/setup-node@v4 # 2nd step: sets up a project environment
      with:
        node-version: 22
        cache: 'npm'

    - name: Install dependencies # 3rd step: installs dependencies
      run: npm i

    - name: Build project
      run: npm run build

    - name: Run tests
      run: npm test # 4th step: runs tests, or linter, etc.

    - name: Deploy
      run: echo "Deploy step goes here"
```

---
transition: slide-left
---

# YAML

- A Dash `-` is used to define an array.  
  ```yaml
  colors:
    - red # Use 2 spaces (not tabs) for one indent
    - green
    - blue 
  # JS analogy: `{ "colors": ["red", "green", "blue"] }`
  ```
  ```yaml
  steps:
  - name: Checkout code
    uses: actions/checkout@v4

  - name: Install dependencies
    run: npm install
  # JS analogy: const steps = [
  #   { name: "Checkout code", uses: "actions/checkout@v4" },
  #   { name: "Install dependencies", run: "npm install" }
  # ];
  ```
- Don't use dashes when defining a single object, key-value pairs that aren't inside an array:


---
transition: slide-left
---

# Exercise: How to Build a Simple CI/CD Pipeline (pg.1)

- Go to a Github repo and click `Settings` tab at top right corner
- Left hand menu, click Pages
- Under Build and Deployment > under Branch > change dropdown to "gh-pages" (root folder / )> click Save
- Left hand menu, under Actions > click General > scroll down to Workflow permissions > click Read and Write permissions > click Save
- Open code, and in root folder create `./github/workflows/deploy.yml`:
  ```yml
  name: Deploy React frontend to GitHub Pages

  on:
    push:
      branches:
        - main

  jobs:
  ```

---
transition: slide-left
---

# Exercise: How to Build a Simple CI/CD Pipeline (pg.2)

```yaml
  deploy:
    runs-on: ubuntu-latest # Other options: ubuntu-22.04, windows-latest, windows-2022, macos-latest etc.
    permissions:
      contents: write

    steps:
      # Step 1: Checkout the repository
      - name: Checkout Code
        uses: actions/checkout@v4

      # Step 2: set up latest node env
      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "node"

      # Step 3: Install dependencies
      - name: Install Deps
        run: npm ci # Clean Install: requires package-lock.json, deletes node_modules, faster than npm i
```

---
transition: slide-left
---

# Exercise: How to Build a Simple CI/CD Pipeline (pg.3)

```yaml
    # Step 4: Build project
    - name: Build the site
      run: npm run build

    # Step 5: Deploy to GitHub Pages
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v4
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }} # Context vars
        publish_dir: ./dist # root directory that has index.html/css/js files, OR /dist
```

- Commit the code.  You should see the job running when you go back to the repo
- Go back to home page of repo > click Deployments > click GitHub Pages link to the deployment

---
layout: image-right
transition: slide-left
image: /assets/cicd.png
backgroundSize: 400px 380px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 🔒 [Role-Based Access Control in Node/Express apps](https://medium.com/@jayantchoudhary271/building-role-based-access-control-rbac-in-node-js-and-express-js-bc870ec32bdb)
- 📒 [CI/CD Handbook](https://www.freecodecamp.org/news/learn-continuous-integration-delivery-and-deployment/) 
- 🤖 [Automate CI/CD with GH Actions](https://www.freecodecamp.org/news/automate-cicd-with-github-actions-streamline-workflow/)
- ⚪ [github.dev web-based VS Code editor](https://docs.github.com/en/codespaces/the-githubdev-web-based-editor)
- 🍇 [Github Actions Marketplace](https://github.com/marketplace?type=actions)
- 🧲 [Setting up Workflow with Netlify](https://www.freecodecamp.org/news/what-is-ci-cd/#heading-setting-up-our-workflow)

<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)

---
transition: slide-left
---

# Exercises: Create some custom steps of your own (pg.1)

- Suppose you wanted to see the files after it ran `npm run build`. Add a step that runs any number of terminal commands to your liking.  For example:
  ```yaml
      - name: Show file structure after building
        run: |
          echo "ls -R dist"
          ls -R dist
  ```

- Now when it's redeployed, poke around until you find the logs.  Try to find the result of your terminal commands.

---
transition: slide-left
---

# Exercises: Custom steps (pg.2)

- Check Node and NPM versions
- Add a step that runs eslint successfully `npm run lint` (double check your package.json to verify that there - an entry for "lint")
- Show all environment vars
- Add a step for running our unit tests from last class
- Log current date/time
- Allow a downloadable link to the actual `dist/` from the Actions page upon inspecting logs
  ```yaml
  - name: Upload build artifacts
    uses: actions/upload-artifact@v4
    with:
      name: production-build
      path: dist/
  ```

---
transition: slide-left
---

# Group Exercise: Create custom steps of your own 

- Continue experimenting by creating custom steps of your own
- OR try using a new action from the [Github Actions Marketplace](https://github.com/marketplace)
- Report back any interesting steps/actions you've played with to share with the rest of the class 
  - ex: Try using [Code Coverage Action](https://github.com/marketplace/actions/vitest-coverage-report)
  - ex: Try using [Super-Linter](https://github.com/marketplace/actions/super-linter)

---
transition: slide-left
---

# To install for Next Class

- Install Expo Go
- if on Mac, may need to install XCode