# Create link for authenticate in Laravel without password

This package permit create a link for authenticate without user or password.

## Instalation

This package can be used in Laravel 5.4 or higher.

You can install the package via composer:

```bash
composer require cesargb/laravel-magiclink
```

Now add the service provider in config/app.php file:

```php
'providers' => [
    // ...
    Cesargb\MagicLink\MagicLinkServiceProvider::class,
];
```

You can publish config file with:

```
php artisan vendor:publish --provider="Cesargb\MagicLink\MagicLinkServiceProvider" --tag=config
```
This is the contents of the published config/permission.php config file:

```php
return [
    /*
    |--------------------------------------------------------------------------
    | Application magiclink Table
    |--------------------------------------------------------------------------
    |
    | This is the magiklink table used by the application to save links to the
    | database.
    |
    */
    'magiclink_table' => 'magic_links',
    /*
    |--------------------------------------------------------------------------
    | Application Users Table
    |--------------------------------------------------------------------------
    |
    | This is the users table used by the application to save users to the
    | database.
    |
    */
    'user_table' => 'users',
    /*
    |--------------------------------------------------------------------------
    | Application Primary Key of Users Table
    |--------------------------------------------------------------------------
    |
    | This is the primary key of users table used by the application to save
    | users to the database.
    |
    */
    'user_primarykey' => 'id',
    'token' => [
        /*
        |--------------------------------------------------------------------------
        | Token lifetime default
        |--------------------------------------------------------------------------
        |
        | Here you may specifiy the number of minutes you wish the default token
        | to remain active.
        |
        */
        'lifetime' => 30,
    ],
    'url' => [
        /*
        |--------------------------------------------------------------------------
        | Path to Validate Token and Auto Auth
        |--------------------------------------------------------------------------
        |
        | Here you may specify the name of the path you'd like to use so that
        | the verify token and auth in system.
        |
        */
        'validate_path' => 'magiclink',
        /*
        |--------------------------------------------------------------------------
        | Path default to redirect
        |--------------------------------------------------------------------------
        |
        | Here you may specify the name of the path you'd like to use so that
        | the redirect when verify correct token.
        |
        */
        'redirect_default' => '/',
        /*
        |--------------------------------------------------------------------------
        | Path default to redirect when token is invalid
        |--------------------------------------------------------------------------
        |
        | Here you may specify the name of the path you'd like to use so that
        | the redirect when token is invalid.
        |
        */
        'redirect_error' => 'magiclink/error'
    ],
];
```

You can publish migration with command:

```bash
php artisan vendor:publish --provider="Cesargb\MagicLink\MagicLinkServiceProvider" --tag=migration
```

After the migration has been published you can create the table by running the migrations:

```bash
php artisan migrate
```

## Usage

First add the use Cesargb\MagicLink\Traits\HasMagicLink trait to your User model(s):

```php
use Illuminate\Foundation\Auth\User as Authenticatable;

use Cesargb\MagicLink\Traits\HasMagicLink;

class User extends Authenticatable
{
    use HasMagicLink;

    // ...

```

This package allows for users to be associated with magiklick.

After add this trait, you can create a magiclink for a user, with this command:

```php
$redirect_to='/dashboard';
$minutes_forexpire_link=4320;
$user->create_magiclink($redirect_to,$minutes_forexpire_link);
```

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.