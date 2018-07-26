## Laravel Passport Installation

Note: tested with Laravel 5.6, Passport 6.0

Install Laravel, and create database file.

```
$ laravel new passport

$ cd passport

$ vi .env
DB_CONNECTION=sqlite

$ touch database/database.sqlite
```

Install Laravel Passport

```
$ composer require laravel/passport

$ php artisan migrate

$ php artisan passport:install
```

vi app/User.php

```php
...
use Laravel\Passport\HasApiTokens;

...
class User extends Authenticatable
{
    use Notifiable, HasApiTokens;
```

vi app/Providers/AuthServiceProvider.php

```php
...
use Laravel\Passport\Passport;

...
    public function boot()
    {
        $this->registerPolicies();

        Passport::routes();
    }
```

vi config/auth.php

```php
...
        'api' => [
            'driver' => 'passport',
            'provider' => 'users',
        ],
```

vi app/Http/Kernel.php

```php
...
    protected $middlewareGroups = [
        'web' => [
            // ...
            \Laravel\Passport\Http\Middleware\CreateFreshApiToken::class,
        ],
```

vi resources/assets/js/components/ExampleComponent.vue

```php
...
<script>
    export default {
        mounted() {
            console.log('Component mounted.')

            axios.get('/api/user')
                .then(response => {
                    console.log(response.data);
                });

        }
    }
</script>
```

Create view
```
$ php artisan make:auth


$ vi resources/views/home.blade.php
...
<div class="container">
    <div class="row justify-content-center">
        <example-component></example-component>

$ npm install

$ npm run dev

$ php artisan serve

```

Browse to http://127.0.0.1:8000, then you should see user data in the browser console.
