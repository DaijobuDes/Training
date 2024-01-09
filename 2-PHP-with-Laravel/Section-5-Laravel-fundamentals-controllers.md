# Controllers

## Exploring controllers
- Creating a controller can be created using `php artisan make:controller <controller_name>`.
- Adding `--resource` argument generates methods inside the class for use as a resource.

## Changes in controllers in Laravel 8
- Old code: `Route::get('/', 'HomeController@index')`
- New code: `Route::get('/checking', '\App\Http\Controllers\HomeController@index');`
- Other methods
```php
    use App\Http\Controllers\HomeController; //

    Route::get('/', [EdwinsController::class, 'index']);
```

## Using controllers
- Used in routes, syntax is show above
- Adding parameters to routes
```diff
web.php
- Route::get('/post', '\App\Http\Controllers\PostController@index');
+ Route::get('/post/{id}', '\App\Http\Controllers\PostController@index');

PostController.php
-    public function index()
+    public function index($id)
     {
-        return 1;
+        return $id;
     }

```
- Resource controllers, a special static function like GET, that gives access to automatically two different types of routes.
- Automatically generates endpoints based on the methods inside the controller class.
