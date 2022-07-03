# Cagtu Code of Conducts (VCS/SCM Guidelines)

**Table of Contents**
- [Cagtu Code of Conducts (VCS/SCM Guidelines)](#cagtu-code-of-conducts-vcsscm-guidelines)
    - [Introduction to Version Control System](#introduction-to-version-control-system)
    - [Repository Management](#repository-management)
        - [Namespace Management](#namespace-management)
        - [Permission Management](#permission-management)
    - [Git Best Practices](#git-best-practices)
        - [Branching and merging](#branching-and-merging)
        - [Committing](#committing)
            - [Rules for committing](#rules-for-committing)
            - [Examples of good commit messages](#examples-of-good-commit-messages)
    - [FAQs](#faqs)

## Introduction to Version Control System

Version Control System(VCS) or Source Control Management(SCM) is a practice of tracking and managing changes to the
source code we write. VCS helps collaborators push their changes staying in different branches without affecting the
original source code. Once the change is accepted, it can be merged to the main branch or a development branch. If
the change is not acceptable, we can completely discard the branch or even remove the branch without affecting the
previous version. To know more about VCS, we can check the links below:

1. https://www.atlassian.com/git/tutorials/what-is-version-control
2. https://about.gitlab.com/topics/version-control/

Some of the popular VCS systems are as follows:

1. [Git](https://git-scm.com/)
2. [Mercurial](https://www.mercurial-scm.org/)
3. [Apache® SVN](https://subversion.apache.org/)

Git is the most sophisticated Source Control management platform that can easily clone, add, push, pull, branch,
merge, and resolve conflicts. Git has covered more than 80% of the market share just because of its robustness. In
our organization, we're going to use git as our base SCM.

This Documentation covers standards for using git at CAGTU which are as follows:

1. creating a project/group name
2. default and protected branches
3. access levels and its audiences
4. Pulling, pushing, and committing practices, etc.

## Repository Management
> _This section is targeted to repository owners and maintainers_

### Namespace Management
Cagtu uses [gitlab](https://gitlab.com) for storing its repositories which is the most featured service provider
among its competitors.

A software organization has many projects in which it has more than one  repository for the project. Github offers a
way to group different projects as groups and individual repo as projects.

An example below shows the hierarchy of projects in an organization:

```
CAGTU
├── buzz-ecommerce
├── cipher-project
├── ...
└── project-n
```
Above projects will have at least 3 subprojects for frontent, backend, and mobile application development. We can
manage this using groups, sub-groups, and projects.

An example is shown in the tree below:

```
CAGTU (gitlab namespace/group)
├── np (gitlab subgroup)
│   ├── buzz-ecommerce (gitlab subgroup)
│   │   ├── buzz-api (individual repository/project)
│   │   ├── buzz-ui (individual repository/project)
│   │   └── buzz-mobile (individual repository/project)
│   ├── ...
│   │
│   └── cipher (gitlab subgroup)
│       ├── cipher-api (individual repository/project)
│       ├── cipher-ui (individual repository/project)
│       └── cipher-mobile (individual repository/project)
│
└── aus (gitlab subgroup)
    ├── project-a (gitlab subgroup)
    │   ├── project-a-api (individual repository/project)
    │   ├── project-a-ui (individual repository/project)
    │   └── project-a-mobile (individual repository/project)
    └── ...


```

The project managed this way would be less cluttered and a lot easier to manage and give
permissions to developers and team-leads at different levels.

For Example:

- `cagtu`
  - `cagtu`/`np`
    - `cagtu`/`np`/`buzz`
        - `cagtu`/`np`/`buzz`/`buzz-api`
        - `cagtu`/`np`/`buzz`/`buzz-ui`
    <br><br>
    - `cagtu`/`np`/`cipher`
        - `cagtu`/`np`/`cipher`/`cipher-api`
        - `cagtu`/`np`/`cipher`/`cipher-ui`

example urls would be:
- https://gitlab.com/cagtu/np/buzz/buzz-ui
- https://gitlab.com/cagtu/np/buzz/buzz-mobile
- https://gitlab.com/cagtu/aus/prj/prj-api
- https://gitlab.com/cagtu/aus/prj/prj-ui


### Permission Management
_This section is targeted to repository owners and maintainers_

Suppose we have the following project hierarchy:

```
CAGTU [Level 1]
├── np [Level 2]
│   ├── buzz-ecommerce [Level 3]
│   │   ├── buzz-api [Level 4]
│   │   ├── buzz-ui  [Level 4]
│   │   └── buzz-mobile  [Level 4]

```

- The **Level 1** group `CAGTU`: will be available to the organization manager and other Technological officers
  with the owner/manager access.
- The **Level 2** group `np`: will be accessible to the nepal-based organization managers and technological officers
  with the owner/manager access.
- The **Level 3** group `buzz-ecommerce`: will be accessible to the team leads of `buzz-ecommerce` with the
  manager access so that they do not need to be reassigned to another repositories of the same project.
- The **Level 4** group `buzz-api`: will be accessible to those developers who works only as `buzz api developers`.
- Similarly, the **Level 4** group `buzz-ui`: will be accessible to those developers who works only as `frontend
  developers` of `buzz-ecommerce` project.

Once we manage the project this way, we can have a clear understanding of assigning and unassigning users to/from a
group.project.

For example, If I want to transfer the team-lead of a project `buzz` to the project `cipher`, then I do not need to
individually add the team-lead to the group, but I can just browse the sub-group `cipher` and add `@team_lead_1` so
that `@team_lead_1` will have access to all the projects inside of the sub_group.

The group/project hierarchy would be as follows

- **Cagtu** (CEO, CTO, Managers)
    - **NP** (Nepal-based Person In-charge, Managers)
        - **Buzz Ecommerce** (`buzz` Team Leads)
            - Buzz API (`buzz` Backend Devs)
            - Buzz UI (`buzz` Frontend Devs)
            - Buzz Mobile (`buzz` Mobile Devs)
        - **Cipher** ( `cipher` Team Leads)
            - Cipher API (`cipher` Backend Devs)
            - Cipher UI (`cipher` Frontend Devs)
            - Cipher Mobile (`cipher` Mobile Devs)

## Git Best Practices

### Branching and merging

### Committing

The git commit should follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) structure.
It should contain a title or summary, and optional body text
1. title or summary
    1. should include `type`, `optional scope`, and `description` of the commit message
    2. recommended: max 50 characters
    3. limit: 72 characters
2. body (if needed only)
    1. recommended: max 72 characters
    2. limit: no

**Commit Types**:
- `build`: a commit that affects the build system or external dependencies
- `ci`: a commit that changes the CI configuration and files
- `docs`: a commit that adds/changes only documentation to the existing code
- `feat`: a commit that adds/removes new feature to the project
- `fix`: a commit that fixes previous issues/bugs (if available mention issue number)
- `perf`: a commit that improves performance
- `refactor` / `style`: a commit that neither adds new feature nor fixes a bug (Eg: whitespace, formatting, etc.)
- `revert`: a commit that reverts previous commit (should include previous hash)
- `test`: a commit that adds or corrects existing tests

**Commit Scopes**:

The scope should mention where the code is changed. Scope generally mentions the name of app, module, or a package.
For example if we're working on authentication module, the name of scope might be `auth`.

> **Note**:  useing `!` after commit type or scope will draw attention that the commit contains **BREAKING CHANGES**

**Commit message structure:**
```
<type>(<scope>): commit message

optional body

optional footer
```
#### Rules for committing
1. Write meaningful commit messages
    - do not commit with texts like `Dummy Commit`, `test commit`, etc.
    - if you have such commits, you can rebase your commits before sending your code to review
2. Commit early, commit often, and commit with clean and purposeful message
    - Do not wait a whole day to commit.
    - As soon as you complete your task (1 purpose), you should commit
    - do not commit for multiple tasks, otherwise rejecting one feature rejects another too.
3. Don't commit generated files
    - Generated files such as `**lock`, `__**cache__`, etc. should be avoided since these files
      generates differently on different systems and causes conflict when merging with others' codes.
4. Do not forget to add `issue numbers` or `ticket numbers` so that it can be tracked easily.
5. Mention the type of commit Example: `feature`, `bugfix`, `documentation`, `test`, etc.

#### Examples of good commit messages


**Example Commit 1**: simple commit message
```
feat: add product list API
```

**Example Commit 2**: simple commit message with scope **(Recommended)**
```
feat(product): add product list API
```

**Example Commit 3**: commit message with commit body
```
feat(product): add model product

adds functionality of product CRUD tools by which inventory/store can be managed.
```

**Example Commit 4**: commit message with body, and issue id
```
fix(transaction): removes 504 error when purchasing multiple items

fixes bug #12345
```

**Example Commit 5**: commit with warning
```
feat(stock)!: add stock models and APIs

BREAKING: existing products in database should have the stock detail otherwise product get api results in 404 errors.
```

## FAQs

1. How can I commit with commit title and body?

   _We can commit title as a regular commit message followed by another `-m` argument for a commit body._
   Example:
   ```shell
   $ git commit -m "feat(product): add products model" -m "my description goes here"

   $
   ```

   **Note:**: _We can use any number of `-m` flags for adding new lines to the commit._

   Alternatively, we can also use enter key if we start our message with double quotes. with this method the terminal automatically adds `>` or `>>` key depending on the operating system to show that the current statement is not terminated.

   Example:
   ```shell
   $ git commit -m "feat(product): add products model
   >> my description goes here."

   $
   ```
