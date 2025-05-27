# Music Tab
A user-friendly web application designed to manage song tabs efficiently, built with Ruby on Rails.

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Instructions](#instructions)
- [Configuration](#configuration)
- [Contributing](#contributing)
    - [Coding Conventions](#coding-conventions)
    - [Branch Naming Conventions](#branch-naming-conventions)
    - [Pull Request Process](#pull-request-process)
    - [Running Tests](#running-tests)
- [Entity Relationship Diagram](#entity-relationship-diagram)
- [Troubleshooting](#troubleshooting)
- [Visual Aids](#visual-aids)
- [API Documentation](#api-documentation)
- [Deployment](#deployment)
- [Contact](#contact)

## Introduction
Managing song tabs on paper can be a consistent struggle for musicians, leading to lost, damaged, or disorganized materials. **Music Tab** offers a digital solution to this problem, providing a centralized space for users to create, organize, view, and edit their song tabs effortlessly. This application is built using Ruby on Rails, leveraging Devise for authentication, Pundit for authorization, and ActionText for rich tab content.

## Prerequisites
Before you begin, ensure you have the following installed:
* Ruby (version `3.2.1` as specified in `.ruby-version`)
* Bundler (gem)
* Node.js and Yarn (for JavaScript asset management and linters)
* SQLite3 (for default development database)
* PostgreSQL (optional for local development, but recommended to mirror production)

## Instructions
To run Music Tab locally:
1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/your_username/music-tab.git](https://github.com/your_username/music-tab.git)
    cd music-tab
    ```
    *(Replace `your_username` with your actual GitHub username or the original repository owner's username if you forked it.)*

2.  **Install Dependencies**
    * Install Ruby gems:
        ```bash
        bundle install
        ```
    * Install JavaScript packages:
        ```bash
        yarn install
        ```

3.  **Environment Variables**
    * This project uses `dotenv-rails`. Copy the example environment file if one exists (e.g., `.env.example`) to `.env` or create a new `.env` file.
    * Ensure `SECRET_KEY_BASE` is set. If not, you can generate one with `rails secret` and add it to `config/credentials.yml.enc` (via `rails credentials:edit`) or to your `.env` file (though credentials are preferred for sensitive keys).
    * For a standard local setup with `config/database.yml` using SQLite, you might not need a `.env` file for database credentials initially.

4.  **Setup the Database**
    * Create the development and test databases (defaults to SQLite as per `config/database.yml`):
        ```bash
        rails db:create
        ```
    * Run database migrations:
        ```bash
        rails db:migrate
        ```
    * Set up sample data for the database (optional but recommended for exploring features):
        * Seed the default admin user:
            ```bash
            rails db:seed
            ```
        * Generate additional sample tabs and users (uses Faker gem, defined in `lib/tasks/dev.rake`):
            ```bash
            rails db:sample_data
            ```

5.  **Start the Server**
    * The `bin/dev` script is recommended for starting the development server (it typically uses Foreman to manage processes like the Rails server and asset compilation if a `Procfile.dev` is used, though one isn't explicitly in your root).
        ```bash
        bin/dev
        ```
    * Alternatively, you can start the Rails server directly:
        ```bash
        rails server
        ```
    * Open your browser and navigate to `http://localhost:3000`.

6.  **Default Admin User**
    * The `db/seeds.rb` file creates an admin user:
        * **Email:** `alice@example.com`
        * **Password:** `password` (Note: The password in `seeds.rb` refers to `Rails.application.credentials.password`. You'll need to set this via `rails credentials:edit` for the seed to work as intended with a secure password).

## Configuration
* **Database:** Configuration is in `config/database.yml`. By default, it uses SQLite3 for development and test environments, and PostgreSQL for production. If you wish to use PostgreSQL locally for development, you'll need to update `config/database.yml` and ensure PostgreSQL server is running.
* **Credentials:** Sensitive information (like `SECRET_KEY_BASE` and potentially production database passwords) is managed via `config/credentials.yml.enc`. Edit this file using `rails credentials:edit`.
* **Devise:** Authentication settings can be found in `config/initializers/devise.rb`.
* **Rails Admin:** Configuration is in `config/initializers/rails_admin.rb`.
* **Blazer:** Configuration is in `config/blazer.yml`.
* **Dotenv:** If you use a `.env` file for local environment variables, `dotenv-rails` will load it.

## Contributing
Contributions are welcome to enhance Music Tab! Please follow these guidelines:

1.  **Fork the Repository**
2.  **Create a New Branch**
    ```bash
    git checkout -b feature/your_feature_name
    ```
    *(See [Branch Naming Conventions](#branch-naming-conventions) below).*
3.  **Make Your Changes**
    * Ensure your code adheres to the [Coding Conventions](#coding-conventions).
4.  **Commit Your Changes**
    * Write clear and concise commit messages.
5.  **Push to the Branch**
    ```bash
    git push origin feature/your_feature_name
    ```
6.  **Create a Pull Request**
    * Provide a detailed description of the changes you've made.
    * Reference any related issues (e.g., "Fixes #123").
7.  **Code Review**
    * Participate actively in the code review process and address any feedback.

### Coding Conventions
* Follow the [Ruby Style Guide](https://rubystyle.guide/) and the project's `.rubocop.yml` for Ruby code.
* Adhere to JavaScript best practices and the project's `eslint.config.mjs` for JavaScript code.
* Ensure all code is well-documented where necessary.
* Write tests for new features and bug fixes.

### Branch Naming Conventions
* Use descriptive names for branches. Suggested formats:
    * Features: `feature/brief-description-of-feature` (e.g., `feature/add-dark-mode`)
    * Bugfixes: `bugfix/issue-number-short-description` (e.g., `bugfix/42-fix-login-redirect`)
    * Chores/Refactoring: `chore/task-description` (e.g., `chore/update-dependencies`)

### Pull Request Process
* Create a pull request targeting the `main` branch (or the current development branch).
* Ensure the PR title and description are clear and informative.
* Verify that all automated checks (CI builds, linters) pass.
* The PR will be reviewed, and once approved and all checks pass, it will be merged.

### Running Tests
* This project uses RSpec for testing. To run the test suite:
    ```bash
    bundle exec rspec
    ```

## Entity Relationship Diagram
The Entity Relationship Diagram (ERD) illustrates the database schema and relationships between models.
*(Ensure `erd.png` is in the root of the repository or update the path below if it's located elsewhere, e.g., `app/assets/images/ERD.png`)*
<img src="erd.png" alt="Entity Relationship Diagram Image"/>

## Troubleshooting
* **Unable to start the Rails server (`bin/dev` or `rails server`):**
    * Ensure all prerequisites (Ruby, Bundler, Node.js, Yarn) are installed correctly and their versions match project requirements if specified.
    * Check for missing environment variables (though for basic local setup, defaults might work).
    * Make sure `bundle install` and `yarn install` completed without errors.
    * Ensure no other process is using port 3000.
* **Database connection errors:**
    * **SQLite (Development Default):** Ensure the `db/development.sqlite3` file has correct permissions.
    * **PostgreSQL (Production/Optional Dev):** Verify your PostgreSQL server is running. Check connection details in `config/database.yml` or your `.env` file. Ensure the database roles and databases exist and you have correct permissions.
    * Run `rails db:setup` (which runs `db:create`, `db:schema:load`, `db:seed`) or `rails db:create db:migrate db:seed` individually.
* **How do I reset the database?**
    * This command will drop the database, recreate it, load the schema, and run the seeds. Use with caution, especially if you have important local data.
        ```bash
        rails db:reset
        ```

## Visual Aids
Demonstrations of key application features:

**View all tabs created**
<img src="app/assets/images/viewTabs.gif" alt="Animated GIF showing the list of all created tabs with search and pagination."/>

**Create a new tab**
<img src="app/assets/images/createTab.gif" alt="Animated GIF demonstrating the process of creating a new song tab using the rich text editor."/>

**View a song tab**
<img src="app/assets/images/viewTab.gif" alt="Animated GIF showing the display of a single song tab with its content and auto-scroll feature."/>

**Edit an existing tab**
<img src="app/assets/images/editTab.gif" alt="Animated GIF demonstrating how to edit an existing song tab's title and content."/>

## API Documentation
Music Tab currently does not expose its own public API endpoints for third-party integrations.

## Deployment
This application is configured for deployment on [Render](https://render.com/) using the `render.yaml` file and associated build/start scripts in the `bin/` directory. It utilizes a PostgreSQL database on Render.
The CI pipeline (`.github/workflows/rails_ci.yml`) also uses PostgreSQL for testing.

## Contact
For any questions, suggestions, or to report issues, please reach out to: bennyjoram@gmail.com or open an issue on this GitHub repository.
