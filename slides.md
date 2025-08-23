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
- Junior, Intermediate, Senior, Tech Lead, Manager, Staff, Director, VP

---
transition: slide-left
---

# What is CI/CD?
Continuous Integration, Continuous Delivery, Continuous Deployment

- Continuous Integration:
  - Changes are committed regularly
  - Unit tests are run
  - Goal: identify problems early
- Continuous Delivery:
  - Automated build processes
  - Software is ready for release
  - Goal: always have a version of software that can be deployed
- Continuous Deployment:
  - Fully automated deployment to prod environments
  - rapid reliable development cycles

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
name: Node.js CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

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
layout: image-right
transition: slide-left
image: /assets/addy.png
backgroundSize: 400px 300px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:
- 👩‍💻 [NeetCode](https://www.freecodecamp.org/news/prepare-for-technical-interviews-using-neetcode-150)

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