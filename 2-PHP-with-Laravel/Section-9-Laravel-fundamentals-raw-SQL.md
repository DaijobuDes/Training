# Raw SQL Queries

## Creating/Inserting Data
- On `routes.php` file
```diff
 Route::get('/insert', function() {

+    DB::insert('INSERT INTO posts (title, content) VALUES (?, ?);', ['PHP with laravel', 'PHP laravel is the best thing that has happened']);

});
```

## Reading data
```diff
 Route::get('/read/{id}', function($id) {

+    $result = DB::select('SELECT * FROM posts WHERE id = ?', [$id]);

-    // return $result;

+    return $result[0]->title;

-    // foreach ($result as $post) {
-    //     $post;
-    // }

-    // return var_dump($result);

});
```

## Updating data
```diff
 Route::get('/update', function() {

+    $result = DB::update('UPDATE posts SET title = ? WHERE id = ?', ['Updated title', 1]);

+    return $result ? "true" : "false";
 });
```

## Deleting data
```diff
 Route::get('/delete/{id}', function($id) {

+    $result = DB::delete('DELETE FROM posts WHERE id = ?', [$id]);

+    return $result ? "true" : "false";
 });
```
