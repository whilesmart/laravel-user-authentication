# Whilesmart Laravel User Authentication Package

This Laravel package provides a complete authentication solution with registration, login, password reset, and OpenAPI
documentation, all ready to use out of the box.

## Features

* **Ready-to-use authentication endpoints:**
    * Registration (first\_name, last\_name, email, phone)
    * Login
    * Password reset (forgot password, reset password)
* **OpenAPI documentation:** Automatically generated documentation using PHP attributes.
* **Customizable user model:** Includes `phone` field.
* **Verification interface:** Enables custom verification logic (e.g., email verification).
* **Configuration file:** Easily customize settings.
* **Laravel agnostic considerations:** designed with future framework agnosticism in mind.

## Installation

### 1. Require the package:

   ```bash
   composer require whilesmart/laravel-user-authentication
   ```

### 2. Publish the configuration and migrations:

You do not need to publish the migrations and configurations except want to make modifications. You choose to publish
the migrations, routes, controllers separately or all at once.

#### 2.1 Publishing only the routes

Run the command below to publish only the routes.

```bash
php artisan vendor:publish --tag=user-authentication-routes
php artisan migrate
```

The routes will be available at `routes/user-authentication.php`. You should `require` this file in your `api.php` file.

```php
    require 'user-authentication.php';
```

#### 2.2 Publishing only the migrations

If you would like to make changes to the migration files, run the command below to publish only the routes.

```bash
php artisan vendor:publish --tag=user-authentication-migrations
php artisan migrate
```

The migrations will be available in the `database/migrations` folder.

#### 2.3 Publish only the controllers

To publish the controllers, run the command below

```bash
php artisan vendor:publish --tag=user-authentication-controllers
php artisan migrate
```
The controllers will be available in the `app/Http/Controllers/Api/Auth` directory.
Finally,  change the namespace in the published controllers to your namespace.

*Note: Publishing the controllers will also publish the routes. See section 2.1*

#### 2.4 Publish everything

To publish the migrations, routes and controllers, you can run the command below

```bash
php artisan vendor:publish --tag=user-authentication
php artisan migrate
```
*Note: See section 2.1 above to make the routes accessible*

### 3. Updates to the User model:
Add the following to the `$fillable` variable in your User model: `  'first_name',
'lsat_name',
'username',
'phone'`


3. **Implement Verification (Optional):**
    * Create a class that implements `Whilesmart\Laravel\User\Authentication\Interfaces\VerifierInterface`.
    * Bind your implementation in a service provider.
    * Configure the verification setting in `config/authentication.php`.

## Usage

After installation, the following API endpoints will be available:

* **POST /api/register:** Register a new user.
* **POST /api/login:** Log in an existing user.
* **POST /api/password/forgot:** Request a password reset.
* **POST /api/password/reset:** Reset a password.
* **OpenAPI Documentation:** Accessible via a route that your OpenAPI package defines.

**Example Registration Request:**

```json
{
    "first_name": "John",
    "last_name": "Doe",
    "email": "[email address removed]",
    "phone": "+15551234567",
    "password": "password123",
    "password_confirmation": "password123"
}
