# Manage the Database

## Quick Setup

Create a local database.

Example:

```sql
CREATE DATABASE example_project;
```

Update `.env`.

```dotenv id="xy3qmk"
DB_HOST=db
DB_PORT=3306

DB_DATABASE=example_project

DB_USERNAME=example_user

DB_PASSWORD=example_password
```

Import the database.

```bash id="4n5l8v"
mysql -u example_user -p example_project < database/schema.sql
```

(Optional) Import seed data.

```bash id="q4sjg6"
mysql -u example_user -p example_project < database/seed.sql
```

Verify the connection.

```bash id="u2ukci"
docker compose ps
```

Open the application and confirm it can access the database.

---

# Complete Guide

The project source code is stored in Git.

The database is **not**.

Each developer should have their own local database so they can develop and test without affecting other developers.

The production database should never be used for development.

---

## Step 1 — Create the Database

Create a new database.

Example:

```sql
CREATE DATABASE example_project;
```

Or create it using phpMyAdmin, MySQL Workbench, or another database management tool.

### Why?

Each developer should have an independent database.

This prevents one developer's testing from affecting another developer's work.

---

## Step 2 — Configure the Connection

Open `.env`.

Example:

```dotenv id="2fxmtt"
DB_HOST=db

DB_PORT=3306

DB_DATABASE=example_project

DB_USERNAME=example_user

DB_PASSWORD=example_password
```

Update the values for your local environment.

Save the file.

Restart the application if required.

```bash id="p0e54z"
docker compose restart
```

---

## Step 3 — Import the Database Schema

Most projects include a schema file.

Example:

```text id="pjlwmn"
database/

schema.sql
```

Import it.

```bash id="3e4ikd"
mysql -u example_user -p example_project < database/schema.sql
```

### What is a schema?

The schema creates the database structure.

It includes:

* Tables
* Columns
* Indexes
* Constraints
* Relationships

The schema does **not** normally include application data.

---

## Step 4 — Import Seed Data (Optional)

Some projects provide sample data.

Example:

```text id="hby1ud"
database/

seed.sql
```

Import it.

```bash id="2wx6u9"
mysql -u example_user -p example_project < database/seed.sql
```

### What is seed data?

Seed data provides example records for development and testing.

Examples:

* Administrator account
* Test users
* Categories
* Sample products

Seed data should never contain production information.

---

## Step 5 — Verify the Database

Open the application.

Confirm:

* Login works.
* Records are displayed.
* New records can be created.
* Existing records can be edited.
* Records can be deleted.

If all operations succeed, the database connection is working correctly.

---

## Step 6 — Share Database Changes

When you change the database structure:

Export the updated schema.

Example:

```bash id="qeqb2q"
mysqldump --no-data example_project > database/schema.sql
```

Commit the updated schema.

```bash id="a18cxh"
git add database/schema.sql

git commit -m "Add orders table"

git push
```

Do **not** export production data unless it is specifically intended as seed data.

---

## Step 7 — Backup the Database

Create a backup.

```bash id="n0yw4k"
mysqldump example_project > backup.sql
```

Restore a backup.

```bash id="9w28kn"
mysql example_project < backup.sql
```

Regular backups protect against accidental data loss during development.

---

# Recommended Project Structure

```text id="vpxwlu"
database/

schema.sql
seed.sql
migrations/
```

| File          | Purpose                      |
| ------------- | ---------------------------- |
| `schema.sql`  | Database structure           |
| `seed.sql`    | Sample development data      |
| `migrations/` | Incremental database changes |

---

# Verification

Verify the database connection.

Open the application.

Check that:

* The application starts.
* The database connects.
* Tables exist.
* Records can be created and updated.

If using Docker:

```bash id="j2u5md"
docker compose ps
```

Confirm the database container is running.

---

# Common Problems

## Access denied

Verify:

```dotenv id="3z4q80"
DB_HOST

DB_PORT

DB_DATABASE

DB_USERNAME

DB_PASSWORD
```

Then restart the application.

```bash id="0xy13t"
docker compose restart
```

---

## Unknown database

The database has not been created.

Create it.

```sql
CREATE DATABASE example_project;
```

Then import the schema again.

---

## Table does not exist

Import the latest schema.

```bash id="v4r4ps"
mysql -u example_user -p example_project < database/schema.sql
```

---

## Accidentally modified production data

Never connect your development environment to the production database.

Always use a dedicated local database for development.

---

# Best Practices

* One local database per developer.
* Never use the production database for development.
* Keep database credentials in `.env`.
* Commit schema changes.
* Never commit production data.
* Backup databases before major changes.

---

# Summary

After completing this guide:

* You can create and configure a local database.
* You understand the difference between schema and data.
* You know how to share database structure with other developers.
* You know how to back up and restore databases.
* You know how to avoid common database mistakes.

Next:

➡ **12 - Secure the Project**
