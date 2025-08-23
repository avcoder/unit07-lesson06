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

# Exercise: How to Build a Simple CI/CD Pipeline

- Go to a Github repo and click `Settings` tab at top right corner
- Left hand menu, click Pages
- Under Build and Deployment > under Branch > change dropdown to "main" > click Save
- Left hand menu, under Actions > click General > scroll down to Workflow permissions > click Read and Write permissions > click Save
- Open code, and in root folder create `./github/workflows/deploy.yml`:
  ```yml
  name: Deploy React frontend to GitHub Pages

  on:
    push:
      branches:
        - main

  jobs:
    deploy:
      runs-on: ubuntu-latest # Other options: ubuntu-22.04, windows-latest, windows-2022, macos-latest etc.        
  ```

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

<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)

---
transition: slide-left
---

# To install for Next Class

- Install Expo Go
- if on Mac, may need to install XCode