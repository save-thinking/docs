# Project Guidelines &middot; 
> Here's a list of guidelines that follow through the course of our project.

<hr>

- [Git](#git)
  - [Some Git rules](#some-git-rules)
  - [Git workflow](#git-workflow)
  - [Writing good commit messages](#writing-good-commit-messages)
- [Documentation](#documentation)
- [Environments](#environments)
  - [Consistent dev environments](#consistent-dev-environments)
- [Testing](#testing)
- [Structure and Naming](#structure-and-naming)
- [Code style](#code-style)
  - [Enforcing code style standards](#enforcing-code-style-standards)
- [Logging](#logging)
- [API](#api)
  - [API design](#api-design)
  



<a name="git"></a>

## 1. Git

<a name="some-git-rules"></a>


### 1.1 Some Git rules

- Every new feature will be developed on a feature branch.

  _Why:_

  > This allows feature to be developed in isolation on a dedicated branch rather than the main branch. It allows one to submit multiple pull requests without confusion. It helps us iterate without distrurbing the master branch with potentially unstable, unfinished code. Our master branch is the releasable, stable branch at all times.

- Never push into `main` branch. Make a Pull Request.

  _Why:_

  > Our main branch is protected and doesn't allow self merges. Each PR requires at least 1 approving review. This notifies team members when a feature is complete. It also enables easy peer-review of the code and dedicates forum for discussing the proposed feature.

- Update your local `feature` branch and do an interactive rebase before pushing your feature and making a Pull Request.

  _Why:_

  > Rebasing will apply your local commits on the top of the commits of the requested branch (`main`) without creating a merge commit. This will also help you look at the merge conflicts and resolve before pushing changes to the remote.

- Resolve potential conflicts while rebasing and before making a Pull Request.
- Delete local and remote feature branches after merging.

  _Why:_

  > As number of features increase, maintaing the feature branches will be an unnecessary overhead. Feature branches only exist while the feature is still under development and gets deleted as soon as the PR is merged to the release branch.

- Before making a Pull Request, make sure your feature branch builds successfully and passes all tests.

  _Why:_

  > As discussded, main branch is our stable branch. If the feature-branch tests fail, there is a high chance that the destination branch build will fail too. 

- Use [this](./.gitignore) `.gitignore` file.

  _Why:_

  > It already has a list of system files that should not be sent with your code into a remote repository. In addition, it excludes setting folders and files for most used editors, as well as most common dependency folders. We want to maintain a consistent development environment for all developers, so avoid pusing redundant local IDE specific files.

- Protect your `main` branch.

  _Why:_

  > It protects our releasable branch from unexpected changes.  

<a name="git-workflow"></a>

### 1.2 Git workflow

Because of most of the reasons above, we use [Feature-branch-workflow] with [Interactive Rebasing] and some elements of [Gitflow] (naming). The steps we follow:

- For a new project, initialize a git repository in the project directory. **Only needed when setting up project for the first time**.

  ```sh
  cd <project directory>
  git init
  ```

- Checkout a new feature/bug-fix branch.
  ```sh
  git checkout -b <branchname>
  ```
- Make code changes.

  ```sh
  git add <file1> <file2> ...
  git commit
  ```
 
  - You should add only files that make up a small and coherent change.
  - Avoid pushing many changes at once. Try to break the PR into cohesive smaller units.


- Sync with remote to get changes you’ve missed.
  ```sh
  git checkout main
  git pull
  ```
  _Why:_
  > This will give you a chance to deal with conflicts on your machine while rebasing (later) rather than creating a Pull Request that contains conflicts.
- Update your feature branch with latest changes from main by interactive rebase.
  ```sh
  git checkout <branchname>
  git rebase main
  ```
- In case of conflicts, resolve them and continue rebase.
  ```sh
  git add <file1> <file2> ...
  git rebase --continue
  ```
- Push your branch. 
  ```sh
  git push -f
  ```
- Make a Pull Request.
- Pull request will be accepted, merged and closed by a reviewer.
- Remove your local feature branch if you're done.

  ```sh
  git branch -d <branchname>
  ```

  to remove all branches which are no longer on remote

<a name="writing-good-commit-messages"></a>

### 1.3 Writing good commit messages

Having a descriptive commit message which explains the issue being addressed is very important. It makes collaborating and understanding the changes easier.

- It is important to note that commits should be as fine-grained and focused as possible, it is not the place to be verbose.

- Use the body to explain more details. 

<a name="documentation"></a>

## 2. Documentation

- Keep `README.md` updated as a project evolves.
- Add meaningful comments to your code. Don't state the obvious. Try to add comments which explaining the critical pieces. 
- Name the functions and variables such that they are self-explanatory. If they are not, make sure you add a comment explaining where and how they are being used.

<a name="environments"></a>

## 3. Environments
<a name="consistent-dev-environments"></a>

### 3.1 Consistent dev environments:

- Set your dependency versions in `package.json`.

  _Why:_

  > It lets others know the version of dependency the project works on. We want the code to behave as expected and identical in any development machine


- Use local modules instead of using globally installed modules.



<a name="testing"></a>

## 5. Testing

- Write testable code, avoid side effects, extract side effects, write pure functions

  _Why:_

  > Tests should run as separate units from the business logic. We want our code to be deterministic and tests help us achieve that.

- Run tests locally before making any pull requests to `main`.

  _Why:_

  > We don't want the releasable branch to be disturbed at any point. Make sure to run your tests after your `rebase` and before pushing your feature-branch to a remote repository.

- Document the test related details in the `README.md` file, if applicable.

<a name="structure-and-naming"></a>

## 6. Structure and Naming

- We structure the directories based on the different modules of our project. This helps organize modules and reduce cluttering.

  **Bad**

  ```
  .
  ├── controllers
  |   ├── product.js
  |   └── user.js
  ├── models
  |   ├── product.js
  |   └── user.js
  ```

  **Good**

  ```
  .
  ├── product
  |   ├── index.js
  |   ├── product.js
  |   └── product.test.js
  ├── user
  |   ├── index.js
  |   ├── user.js
  |   └── user.test.js
  ```

- Put your scripts in a `./scripts` folder. This includes `bash` and `shell` scripts.
- We create a separate docs repo for storing all design documents and ADRs. 

<a name="code-style"></a>
## 7. Code style

<a name="enforcing-code-style-standards"></a>
### 7.1 Enforcing code style standards

- TBA (any specific enforcements added to CI/CD pipeline eg linting, etc) 


<a name="logging"></a>

## 8. Logging



- Avoid console log statements in production, keep it restricted to local development, remove such statements before changes are committed remotely.

  _Why:_

  > Even though your build process can (should) get rid of them, make sure that your code style checker warns you about leftover console logs.

- Use of standard logging library for easier indexing. As a future scope of the project, we plan on integrating the logs for Splunk for monitoring and alerts.

<a name="api"></a>
## 9. API

<a name="api-design"></a>
### 9.1 API design

_Why:_

> For our APIs, the first step is to document the API details in an SIA(Service Integration Agreement). This document can be used by team members and clients for simple and consistent consumption.

_Why:_

> Lack of consistency and simplicity can massively increase integration and maintenance costs. Which is why `API design details` is included in this document.

- The SIA would comprise of details like the URL, the paramaters expected(if any), the request payload, the response payload, and short description.
- Pagination, filtering, and sorting don’t need to be supported from start for all resources. We work on these incrementally through the course of our project.



