# Cagtu Code of Conducts (VCS/SCM Guidelines)

**Table of Contents**
- [Cagtu Code of Conducts (VCS/SCM Guidelines)](#cagtu-code-of-conducts-vcsscm-guidelines)
    - [Introduction to Version Control System](#introduction-to-version-control-system)
    - [Repository Management](#repository-management)
        - [Namespace Management](#namespace-management)
        - [Permission Management](#permission-management)

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
