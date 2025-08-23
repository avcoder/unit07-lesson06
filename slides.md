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
- Intermediate: 3-4 years
- Senior: 5-8 years
- Tech Lead 8+ years
- Manager 10+ years
- Staff: how well can you communicate/get along with senior leadership?
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

- Build phase: as soon as you push code to repo, that event triggers an automatic `npm run build`, this is where the code and its dependencies are compiled into a single executable
- Test phase: The build is tested to ensure no errors in Unit Tests, Linting, Typescript, etc.
- Staging: The app is run in a production-like environment (ex: a temporary url) that devs can test to ensure it's ready for prod
- Deployment: App is automatically deployed to end-users

<img src="/assets/cicd2.webp" style="height: 250px" >

---
transition: slide-left
---

# Github Actions
an automation framework for software workflows

- Workflows are coded in yaml and stored .github/workflows/ in your repo
- Events are the triggers (new push, PR, new issue etc) that run a workflow
- Runners are compute layers (ex: ubuntu, windows, macos) and come with preinstalled tools, compilers.
- Each workflows has one or more jobs.  Jobs are high-level tasks that uses steps (simple commands, scripts, actions)
- Actions are useful for running common tasks in repeatable fashion
- Depending on the kind of files you have in your repo, Github can suggest which starter workflow works best to build, package and deploy your code

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

    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v4 # 2nd step: sets up a project environment
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'

    - name: Install dependencies # 3rd step: installs dependencies
      run: npm ci

    - name: Run tests
      run: npm test # 4th step: runs tests, or linter, etc.
```

---
transition: slide-left
---

# CI for JS

- Let's create a CI workflow that:
  - Git Checks out the code
  - Set up Node.js
  - Build and test project
- Optional: Matrix strategy for multiple versions of Node

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