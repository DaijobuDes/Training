# Database - Eloquent / ORM

- Creating a model `php artisan make:model Posts -m`
- `-m` flag also creates a migration


## Reading data
- Without constraints
```php
use App\Models\Post;

Route::get('/orm-read/{id}', function($id) {

    $result = Post::find($id);

    return $result ? $result : array();

});
```
- With constraints
```php
Route::get('/orm-readwhere/{id}', function($id) {

    $result = Post::where('id', $id)->orderBy('id', 'desc')->take(1)->get();

    // $result = Post::where('is_admin', $id)->orderBy('id', 'asc')->take(10)->get();

    return $result;

});
```
- Other ways to retrieve data
```php
Route::get('/orm-readwhere/{id}', function($id) {

    $result = Post::where('id', $id)->orderBy('id', 'desc')->take(1)->get();

    // $result = Post::where('is_admin', $id)->orderBy('id', 'asc')->take(10)->get();

    return $result;

});

Route::get('/orm-findmore/{id}', function($id) {

    // $result = Post::findOrFail($id);
    $result = Post::where('id', '>=', 1)->firstOrFail();
    return $result;

});
```
- More can be found on the [documentation here](https://laravel.com/api/10.x/Illuminate/Database/Eloquent.html)


## Inserting/creating data
```php
Route::get('/orm-insert', function() {

    // $result = Post::findOrFail($id);
    $post = new Post;
    // $post = Post::find(2);
    $post->title = "New ORM insert query";
    $post->content = "Some data here via ORM query";
    return $post->saveOrFail() ? "true" : "false";

});

Route::get('/orm-insert2', function() {

    // $result = Post::findOrFail($id);
    // $post = new Post;
    $post = Post::find(5);
    $post->title = "yes another method";
    $post->content = "This data here got updated via ORM query";
    return $post->saveOrFail() ? "true" : "false";

});
```

## Mass data assignment
- Going back to Post.php on models
```diff
     protected $primaryKey = 'id';

+    // For mass data assignment
+    protected $fillable = [
+        'title',
+        'content'
+    ];

```
- Adding `protected $fillable` is required to prevent MassAssignmentException.

## Updating data
```php
Route::get('/orm-update', function() {

    $result = Post::where('id', 9)->where('is_admin', 0)->update(['title'=>'New PHP title something', 'content'=>"This is laravel"]);
    return $result ? "true" : "false";

});
```

## Deleting data
```php
Route::get('/orm-delete/{id}', function($id) {

    $result = Post::find($id);
    $result->delete();
    return $result ? "true" : "false";

});

Route::get('/orm-delete2', function() {

    $result = Post::destroy(30); // Array or int
    // Post::where('is_admin', 0)->delete(); // Deletes all is_admin==0
    return $result ? "true" : "false";

});
```
- Can also delete with constraints by bulk or via an array of IDs

## Soft deleting data
- Added `$dates` variable for the use of soft delete
- Basically *trashed* in the database with the `$dates` variable.
```diff
     protected $primaryKey = 'id';

+    protected $dates = ['deleted_at'];

     // For mass data assignment
     protected $fillable = [
         'title',
         'content'
     ];
```
- Created a new migration in order to add a column `deleted_at` by `php artisan make:migration add_deleted_at_column_to_posts_table --table=posts`

## Retrieving soft deleted items
- Using the `all()` method does not include the soft deleted items.
- Using the `withTrashed()` method recovers the soft deleted item and includes the non-soft deleted item.
- Using the `onlyTrashed()` method only returns the soft deleted items.
```php
Route::get('/orm-getsoftdelete/{id}', function($id) {

    $result = Post::withTrashed()->where('id', $id)->get();
    return $result;

});
```

## Restoring soft deleted items
- Using the `restore()` method restores the soft deleted item.
```php
Route::get('/orm-restore', function() {

    $result = Post::withTrashed()->where('is_admin', 0)->restore();
    return $result;

});
```

## Permanently deleting soft deleted items
- Dangerous operation: make sure you used `onlyTrashed()` instead of `withTrashed()`
```php
Route::get('/orm-forcedelete', function() {

    $result = Post::onlyTrashed()->where('is_admin', 0)->forceDelete();
    return $result ? "true" : "false";

});
```
