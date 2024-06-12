# Verse Bytes API

Simple API for my blog using the following technologies:

- [Node](https://nodejs.org/en/)
- [Express](https://expressjs.com/en/api.html)
- [Prisma ORM](https://www.prisma.io/)
- [Railway](https://railway.app/)

## Table of Contents

- [API Overview](#api-overview)
- [Business Objects](#business-objects)
- [Run it locally](#run-it-locally)
- [Deploy it](#deploy-it)

## API Overview

```
    /api
    .
    ├── /auth
    │   └── POST
    │       ├── /login
    |       |__/signup
    ├── /users
    │   └── GET
    │       PUT
    │       DELETE
    │       └── /
    ├── /blog
    │   └── GET
    │       POST
    |       PUT
    |       DELETE
    │       └──/
```

### API Detail

| Method             |                Path                 |                          Purpose |
| :----------------- | :---------------------------------: | -------------------------------: |
| POST               |             /auth/login             |    Validates username & password |
| POST               |            /auth/signup             | Register a user, generate token. |
| GET                |                /blog                |                   Get all blogs. |
| GET                |              /blog/:id              |                  Get blog by id. |
| **PRIVATE ROUTES** | Only accessible for **ADMIN** role: |
| GET                |               /users                |                   Get all users. |
| GET                |             /users/:id              |                  Get user by id. |
| PUT                |             /users/:id              |               Update user by id. |
| DELETE             |             /users/:id              |               Delete user by id. |
| POST               |                /blog                |           Creates new blog post. |
| PUT                |              /blog/:id              |                Update blog post. |
| DELETE             |              /blog/:id              |                Delete blog post. |

---

## Business Objects

### Prisma Schema

- **Users (table)**

  - id (auto-generated)
  - email (string)
  - password ()
  - role (enum)
  - createdAt (Date)
  - updatedAt (Date)
  - authoredPosts (Array of blog posts)

- **Blog Posts(table)**

  - id(auto-generated)
  - title (string)
  - content (string db.Text to ensure large string)
  - author (relationship based on userId foreign key)
  - authorId (integer)
  - createdAt (Date)
  - updatedAt (Date)

- **Subscriber (table)**

  - id(auto-generated)
  - email (string)
  - createdAt (Date)

## Run it locally

To build and run this app locally you will need a few things:

- Install [Git](https://www.git-scm.com/)
- Install [Node](https://nodejs.org/en/)
- Install [PostgreSQL](https://www.postgresql.org/download/) or any DB provider that you want to connect with prisma.

### Getting Started

- Clone the repository

```
git clone https://github.com/mariatorrentedev/verse-bytes.git <project_dir>
```

- Create an `.env` file based on the example

```
mv example.env .env
```

- Install dependencies

```
npm install
```

- Run it

```
npm run dev
```

- Build it

```
npm run build
```

## Deploy it

### Railway

1. Go to your [Railway dashboard](https://railway.app/dashboard).

2. Create a new project and connect it to your current repository, deploy it.

3. Create another service insde the same project for the DB.

**_Note: This repo includes a github workflow that will do CI/CD for both, the DB and the server, in order for it to work we would need to add some secrets to our repo:_**

4. Create a `RAILWAY_TOKEN` https://railway.app/project/<your_project_id>/settings/tokens.

### Github

1. Go to your repository project settings.

2. Under _Security->Secrets and Variables>actions_ add 3 new repository secrets:

   - `RAILWAY_TOKEN` create above.
   - `RAILWAY_SERVICE_ID` cp value under _variables_ in Railway project dashboard.
   - `DATABASE_URL` cp value under _variables_ from the DB service in Railway project dashboard.

3. This workflow will be triggered based on the `master` branch.
