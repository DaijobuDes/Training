# Laravel Fundamentals

## Serving our app
- `php artisan serve`, specifying a listen port is optional

## Laravel structure overview
- `app` folder contains the models and controllers
- `bootstrap` folder contains files where the whole application gets bootstrapped which means that it is going to get things from other files and start the application
- `config` folder contains configuration files of the application
- `database` folder, keeps migrations, help create tables
- `public` folder, for serving files to the public
- `resources` folder, contains files that needs to be compiled
- `routes` folder, mostly on `web.php` it is where one can edit the file to add more routes/endpoints to the application. `api.php` are API endpoints that are not exposed to the public and the application requests data from the application to/from a database
- `tests` folder, containing tests to test the application
- `vendor` folder, contains libraries downloaded from using composer

## Exploring routes
- Requires editing `web.php` on `${workingDirectory}/routes/web.php`
- A basic route can be created by
```php
Route::get('/', function() {
    return "Hello World!";
});
```
- One can add arguments to the function and add dynamic routes on the path set
