# Views

## Exploring views
- Naming convention on adding views must be <filename>.blade.php
- It has its own templating system. Laravel blade templating system.
- To make the view viewable, call by returning a view object `return view('view_page');`

## Passing data to views
- To pass data to views, use `{{` and `}}`, e.g `{{ $id }}` to display the variable.
- For multiple values, we can use in the view e.g `<h1>Post {{ $id }} | {{ $name }} | {{ $password }}</h1>`.
```diff
web.php
+ Route::get('posts/{id}/{name}/{password}', 'App\Http\Controllers\PostController@show_post');

PostController.php
+    public function show_post($id, $name, $password)
-    public function show_post($id)
     {
-        return view('post')->with('id', $id);
+        return view('post', compact('id', 'name', 'password')); // Alternative method to pass values
     }
```
