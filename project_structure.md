# Cagtu Code of Conducts

- [Cagtu Code of Conducts](#cagtu-code-of-conducts)
  - [Project Structure Guidelines](#project-structure-guidelines)
      - [the `README.md` file](#the-readmemd-file)
      - [The `CHANGELOG.md` File](#the-changelogmd-file)
      - [The `.editorconfig` file](#the-editorconfig-file)
      - [The `.gitignore` File](#the-gitignore-file)
    - [The SDLC](#the-sdlc)
    - [Modular structure](#modular-structure)

## Project Structure Guidelines

Each project should follow the basic structure as follows:

```
📂 project
    📂 docs
        📂 res
        📄 doc1.md
        📄 doc2.md
    📄 README.md
    📄 CHANGELOG.md
    ⚙️ .editorconfig
    ⚙️ .gitignore
    ⚙️ .env (git ignored)
    ⚙️ .env.sample
    🐟 Dockerfile (if required)
    🐟 docker-compose.yml (if required)
    ...

```

#### the `README.md` file
Readme.md is a markdown file that contains all the basic requirements related to project setup, development environment, and deployment instructions. It should mention the following:

1. Introduction to the project
   1. name
   2. description
   3. project status
   4. Road maps
2. Setting up the project for the first time
3. Configuring environment variables
4. dependency management and its standards
5. `How To`s
6. `FAQ`s
7. Troubleshooting
8. Testing and Deployment Instructions and standards

#### The `CHANGELOG.md` File

The changelog file tracks all the changes throughout the release.
Generally changelog is modified whenever we add the tags to the commit.

Standards For creating a good changelog file:

- Title should always start with the date in format ( YYYY-MM-DD ) or version number with Semantic versioning ( vX.Y.Z )
- Each change should be added on top of previous changes. (Reverse Chronological Order)
- Once new changelog needs to be maintained, we need to write on top of the previous changelog.

**Example of changelog.md**

```markdown
# CHANGELOG


## 2022-06-25 (V1.0.0)

**Collaborators**
- Team Lead 1(coll1@cagtu.com)
- Team Lead 2(coll2@cagtu.com)

### Changes
1. Description to Change 1 [link ( if needed)](https://foo.bar.com)
2. Description to Change 2 [link to the local file or markdown](./another_file.md)
3. Description to Change 3

<hr>
## 2022-05-25 (V0.9.5)

**Collaborators**
- Team Lead 3(coll1@cagtu.com)
- Team Lead 4(coll2@cagtu.com)

### Changes
1. Description to Change 1 [link Name( if needed)](https://foo.bar.com)
2. Description to Change 2 [link to the local file or markdown](./another_file.md)
3. Description to Change 3
```

#### The `.editorconfig` file
The editor config file is recommended to add configurations to the workspace since different users use different settings to their ide. This file gives more customization to JetBrains IDEs. To know more about editorconfig files, we can browse https://editorconfig.org/.

**Sample editorconfig file:**
```editorconfig
root = true

[*]
charset = utf-8
end_of_line = lf
indent_size = 4
indent_style = space
tab_width = 4
insert_final_newline = true
trim_trailing_whitespace = true
max_line_length = 120
```
To know more about editorconfig, you can check [this **.editorconfig** file](./.editorconfig)

For VS Code, we need to install the official editorconfig plugin to work with editor config files. Plugin Name: `editorconfig.editorconfig`

#### The `.gitignore` File

The gitignore file should follow standard gitignore file guidelines. We can auto generate the gitignore file from the vscode plugin for the respective programming languages.

For collaboration and cross platform solutions, it is not recommended
to IDE settings, locks, and Environment configurations:
- Lock files, Eg: `package-lock.json`, `yarn.lock`, `Pipfile.lock`, etc.
- IDE settings Eg: `.idea`, `.vscode`, etc
- Cache files Eg: `**/__pycache__.`, etc
- dotenv files Eg: `.env`, `.env.local`, etc. We can however add an example of a environment file as a reference. Eg: `.env.sample` can be tracked so that developers can create their own environment files with reference to `.env.sample` file.


### The SDLC

The software development lifecycle should follow the following pattern:

1 Develop
2 Validate on local machine
3 Deploy to test server
4 Validate and QA
5 Refactor
6 Go to step 1
7 If success, release to production

For more details, you can check the following documents:

- [Backend Coding Guidelines](https://docs.google.com/document/d/1URp4ymR3C8rqoYjn-TDHCHrBel71GRQg42441HvlZ8Y)
- [Frontend Coding Guidelines](https://docs.google.com/document/d/1z7cvWywWGqvYkSqxvn07GCObD6Nlul0l2N0fVnaM488)




### Modular structure

**Frontend Specific Structure**

```
📂 project
    📂 components
        📂 foo
            📄 index.ts
            📄 components.tsx
            📄 reducer.tsx
            📄 types.ts
        📂 bar
            📄 index.ts
            📄 components.tsx
            📄 reducer.tsx
            📄 types.ts
        📄 index.ts

```

**Backend Specific Structure**
```
📂 project
    📂 apps
        📂 foo
            🐍 __init__.py
            🐍 apps.py
            🐍 models.py
            ...
        📂 bar
            🐍 __init__.py
            🐍 apps.py
            🐍 models.py
            ...
        🐍 __init__.py

```

