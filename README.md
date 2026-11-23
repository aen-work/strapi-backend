# Book Club

A full-stack book club application with a vanilla HTML/CSS/JavaScript frontend and a Strapi 5 backend.

## Features

- Browse books and open a book details page
- Search and filter the book collection
- Create an account and log in
- Save books to a user profile
- Add ratings from 1 to 10
- Switch between light, dark, and contrast themes
- Manage books, ratings, users, and site settings in the Strapi admin panel

## Project structure

```text
book-club/
├── frontend-cms-project/  # Static frontend
└── strapi-backend/        # Strapi API and admin panel
```

The frontend uses plain HTML, CSS, JavaScript, and Axios. The API configuration is defined in `frontend-cms-project/config.js`.

## Requirements

- Node.js 20 to 24
- npm 6 or newer

## Local setup

### 1. Start the backend

From the repository root:

```powershell
cd strapi-backend
npm install
Copy-Item .env.example .env
npm run develop
```

Strapi will be available at:

- Admin panel: http://localhost:1337/admin
- REST API: http://localhost:1337/api

Create an initial admin account in the admin panel, then create the required content and publish it.

### 2. Start the frontend

From a second terminal at the repository root:

```powershell
cd frontend-cms-project
npx serve .
```

Open the URL printed by `serve` (typically http://localhost:3000).

The frontend expects the Strapi API at http://localhost:1337/api. Update `frontend-cms-project/config.js` if your backend uses another URL.

## Environment variables

Copy `.env.example` to `.env` before starting Strapi. Replace the example secrets with unique values.

The backend supports SQLite by default and stores its local database in `.tmp/data.db`.

For PostgreSQL or MySQL, set `DATABASE_CLIENT` and the corresponding `DATABASE_HOST`, `DATABASE_PORT`, `DATABASE_NAME`, `DATABASE_USERNAME`, and `DATABASE_PASSWORD` variables supported by `config/database.js`.

## Content types

- **Book:** title, author, pages, published date, cover image, saved users, and ratings
- **Rating:** integer value from 1 to 10, linked to a user and book
- **Site setting:** theme and hero image visibility

## API permissions

In Strapi's admin panel, configure permissions under **Settings > Users & Permissions Plugin > Roles**:

- For the public role, allow only the frontend operations needed without authentication.
- For the authenticated role, allow users to read their profile, save books, and create or update ratings.
- Keep write access to books and site settings restricted to authenticated administrators.

## Available backend commands

```powershell
npm run develop   # Start Strapi with hot reload
npm run dev       # Alias for develop
npm run build     # Build the admin panel
npm start         # Start the built application
npm run console   # Open the Strapi console
npm run upgrade   # Upgrade Strapi
```

## Data and uploads

The local SQLite database is at `strapi-backend/.tmp/data.db`. Uploaded media is stored in `strapi-backend/public/uploads`.

Both locations contain local application data and should not be committed to a shared repository. Use Strapi backup or transfer tools before deploying or replacing a database.
