# Laravel Implementation Notes

## Introduction
- **Laravel**: A PHP framework that follows the **Model-View-Controller (MVC)** architecture, designed for rapid and secure web application development.
- **Framework**: A collection of methods, classes, and files that developers use and extend to build applications efficiently.
- **Architecture**: The design pattern a framework follows. Laravel uses MVC architecture.
- **MVC Breakdown**:
  - **Model (M)**: A class handling database interactions (e.g., a `User` model corresponds to a `users` table).
  - **View (V)**: Handles HTML and visual representation seen in the browser.
  - **Controller (C)**: Acts as an intermediary, retrieving data from the model and passing it to the view.

## Features of Laravel
- **Authentication**: Built-in system simplifies user authentication. Configure models, views, and controllers to enable features like login, registration, and password reset (enhanced since Laravel 5).
- **Innovative Template Engine**: Uses **Blade**, enabling dynamic website creation with reusable widgets and solid structures.
- **Effective ORM**: **Eloquent ORM** allows database queries using PHP syntax, mapping tables to models for seamless integration without SQL.
- **MVC Architecture Support**: Facilitates teamwork by separating business logic (controller) from presentation (view), reducing code duplication and enabling parallel development.
- **Secure Migration System**: Manages database schema changes using PHP (migrations), ensuring secure and reliable updates without manual SQL.
- **Unique Unit Testing**: Supports **PHPUnit** for running test cases to verify changes, with the ability to write custom tests.
- **Intact Security**: Provides built-in security features, including:
  - **Bcrypt Hashing Algorithm** for encrypted password storage.
  - Protection against SQL injection, XSS, and CSRF (aligned with OWASP standards).
- **Libraries and Modular**: Includes object-oriented libraries (e.g., authentication, social media login) and pre-installed libraries not found in other PHP frameworks. Modular design supports responsive PHP development.
- **Artisan**: A command-line tool for automating repetitive tasks, generating boilerplate code (e.g., MVC files, migrations), and creating custom commands.

## Topic 1: Installation of Laravel with Prerequisites

### Prerequisites
- Install **Composer** (dependency manager) and **Git** (version control system) before installing Laravel.

#### Composer Installation
- **Overview**: Composer is a dependency manager for PHP, developed by Nils Adermann and Jordi Boggiano (started April 2011, released March 1, 2012). It manages libraries and dependencies via the command line, using **Packagist** as its main repository.
- **Purpose**: Installs dependencies, provides autoloading for libraries, and simplifies package integration.
- **Key Commands**:
  - **require**: Adds libraries to `composer.json` and installs them.
    ```json
    {
        "require": {
            "facebook/php-sdk": "3.2.3"
        }
    }
    ```
  - **install**: Downloads dependencies listed in `composer.json`.
  - **update**: Updates dependencies to the latest versions specified in `composer.json`.
  - **remove**: Uninstalls a library and removes it from `composer.json`.

- **Steps to Install Composer (Windows)**:
  1. Download Composer from: [https://getcomposer.org/download/](https://getcomposer.org/download/).
  2. Run the downloaded `Composer-Setup.exe` file.
  3. Select **Developer mode** and click **Next**.
  4. Choose the installation path and click **Next**.
  5. Specify the PHP command-line path (e.g., `C:\wamp\bin\php\php7.3\php.exe`).
  6. Optionally configure a proxy server (uncheck if not needed) and click **Next**.
  7. Click **Install** when prompted.
  8. Click **Next** and optionally check "View online documentation."
  9. Click **Finish** to complete installation.
  10. Verify installation by opening a command prompt and typing:
      ```bash
      composer
      ```
      - Displays Composer version and commands if successful.

#### Git Installation
- **Overview**: Git is a version control system for tracking code changes and facilitating collaboration.
- **Steps to Install Git (Windows)**:
  1. Download Git from: [https://git-scm.com/downloads/](https://git-scm.com/downloads/).
  2. Select the **Windows** link to start the download.
  3. Run the downloaded file (e.g., `Git-2.23.0-64-bit.exe`).
  4. Click **Next** on the initial setup screen.
  5. Follow prompts to configure options (e.g., default editor, branch name, PATH environment).
  6. Complete installation by clicking **Finish**.
  7. Verify installation by opening a command prompt and typing:
      ```bash
      git --version
      ```
      - Displays Git version if successful.

### Laravel Installation
- **Requirements**:
  - PHP (version 7.3 or higher for recent Laravel versions).
  - Composer installed.
  - Web server (e.g., Apache, Nginx) and database (e.g., MySQL).
- **Steps to Install Laravel**:
  1. Open a command prompt or terminal.
  2. Navigate to the desired project directory:
     ```bash
     cd path/to/your/project
     ```
  3. Install Laravel via Composer:
     ```bash
     composer create-project --prefer-dist laravel/laravel project-name
     ```
     - Replace `project-name` with your desired project folder name.
     - Downloads Laravel and its dependencies.
  4. Navigate to the project directory:
     ```bash
     cd project-name
     ```
  5. Start the Laravel development server:
     ```bash
     php artisan serve
     ```
     - Runs at `http://localhost:8000` by default.
  6. Verify installation by accessing `http://localhost:8000` in a browser to see the Laravel welcome page.

### Additional Setup
- **Environment Configuration**:
  - Copy `.env.example` to `.env`:
    ```bash
    cp .env.example .env
    ```
  - Generate an application key:
    ```bash
    php artisan key:generate
    ```
  - Configure database settings in `.env`:
    ```env
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=your_database_name
    DB_USERNAME=your_database_user
    DB_PASSWORD=your_database_password
    ```
- **Database Setup**:
  - Create a MySQL database:
    ```sql
    CREATE DATABASE your_database_name;
    ```
  - Run migrations to set up database tables:
    ```bash
    php artisan migrate
    ```

## Practical Notes
- **Environment Setup**:
  - Ensure PHP, Composer, and Git are added to the system PATH.
  - Use a local development environment (e.g., XAMPP, WAMP, Laravel Homestead).
- **Security**:
  - Keep `.env` file secure and exclude from version control (add to `.gitignore`).
  - Use strong database credentials and Bcrypt for passwords.
- **Troubleshooting**:
  - Composer issues: Verify PHP version and PATH settings.
  - `php artisan serve` issues: Check for port conflicts (use `--port=8001`).
  - Ensure write permissions for `storage` and `bootstrap/cache` directories.
- **Best Practices**:
  - Use Git for version control.
  - Update dependencies regularly:
    ```bash
    composer update
    ```
  - Explore Artisan commands:
    ```bash
    php artisan list
    ```
- **Testing**:
  - Run default test suite:
    ```bash
    php artisan test
    ```
  - Write custom PHPUnit tests for application features.