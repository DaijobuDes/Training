# Database - Eloquent Relationships

## One-to-one Relationship
- Additions to the `User.php` models
```diff
     protected $casts = [
         'email_verified_at' => 'datetime',
         'password' => 'hashed',
     ];

+    public function post()
+    {
+        // Automatically points to user_id
+        return $this->hasOne('App\Models\Post');
+        // 2nd parameter optional, different id name, e.g the_user_id and so on
+    }
```
- `web.php` routes file
```php
use App\Models\User;

Route::get('/user/{id}/posts', function($id) {

    return User::find($id)->post->title;

});
```

## Inverse relationship
- Additions to the `Post.php` model
```diff
     // For mass data assignment
     protected $fillable = [
         'title',
         'content'
     ];

+    public function user()
+    {
+        return $this->belongsTo('App\Models\User');
+    }
```
- `web.php` routes file
```php
// Inverse relation
Route::get('/post/{id}/user', function($id) {

    return Post::find($id)->user->name;

});
```

## One-to-many relationship
- Additions to `User.php` model
```diff
         return $this->hasOne('App\Models\Post');
         // 2nd parameter optional, different id name, e.g the_user_id and so on
     }

+    public function posts()
+    {
+        return $this->hasMany('App\Models\Post');
+    }
```

- `web.php` routes file
```php
// One-to-many relationship
Route::get('/user/{id}', function($id) {

    $user = User::find($id);

    return $user->posts;
    // foreach ($user->posts as $post) {
    //     echo $post->title.'<br>';
    // }

});
```
- Either return the whole posts unprocessed or echo it out inside a for-each loop.

## Many-to-many relationship
- Using pivot tables, a lookup table to be relayed on other tables
- `php artisan make:model Role -m`, creating a Role table with migrations
- `php artisan make:migration create_users_roles_table --create=role_user`
- For creating the role migrations, the `name` column was added for the role name
```php
    public function up(): void
    {
        Schema::create('roles', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
```
- For the pivot table, `user_id` and `role_id` were added
```php
    public function up(): void
    {
        Schema::create('role_user', function (Blueprint $table) {
            $table->id();
            $table->integer('user_id');
            $table->integer('role_id');
            $table->timestamps();
        });
    }
```
- Some additions to the `User.php` model
```diff
         return $this->hasMany('App\Models\Post');
     }

+    public function roles()
+    {
+        return $this->belongsToMany('App\Models\Role');
+    }
```
- `belongsToMany()` method can take multiple optional arguments. It can take the table name and keys to customize tables names, etc.
```diff
+    return $this->belongsToMany('App\Models\Role', 'user_roles', 'user_id', 'role_id');
```
- Many-to-many relationship route
```php
// Many-to-many relationship
Route::get('/user/{id}/role', function($id) {

    $user = User::find($id);
        // ->roles()->orderBy('id', 'desc')-get();

    foreach ($user->roles as $role) {
        return $role->name;
    }

});
```

## Querying intermediate table
- Additions to `Role.php` model
```diff
 class Role extends Model
 {
     use HasFactory;

+    public function users()
+    {
+        return $this->belongsToMany('App\Models\User');
+    }

}
```
- To retrieve `created_at` or `updated_at`, we use the `withPivot()` method that takes a single string or an array type object.
```diff
         return $this->hasMany('App\Models\Post');
     }

     public function roles()
     {
-        return $this->belongsToMany('App\Models\Role');
+        return $this->belongsToMany('App\Models\Role')->withPivot(['created_at', 'updated_at']);
     }
```
- Accessing the intermediate table (pivot table), basically still requiring to find the user.
```php
// Accessing the intermediate table (pivot table)
Route::get('/user/pivot/{id}', function($id) {

    $user = User::find($id);

    foreach ($user->roles as $role)
    {
        return $role->pivot->created_at;
    }
});
```

## Has-many-through relationships
- `php artisan make:model Country -m`
- `php artisan make:migration add_country_id_column_to_users --table=users`
- Creating a Country table and adding `country_id` to the table Users
```php
    public function up(): void
    {
        Schema::table('users', function (Blueprint $table) {
            $table->integer('country_id');
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::table('users', function (Blueprint $table) {
            $table->dropColumn('country_id');
        });
    }
```
- On the created model with the migration
```php
    public function up(): void
    {
        Schema::create('countries', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
```
- On `web.php` routes file
```php
// Has-many-through relationship
Route::get('/user/country/{id}', function($id) {

    $country = Country::find($id);

    foreach ($country->posts as $post) {
        return $post->title;
    }

});
```

## Polymorphic relationships
- `php artisan make:model Photo -m`
- Create photo migration
```php
    public function up(): void
    {
        Schema::create('photos', function (Blueprint $table) {
            $table->id();
            $table->string('path');
            $table->integer('imageable_id');
            $table->string('imageable_type');
            $table->timestamps();
        });
    }
```
- On the posts migrations
```diff
     public function up(): void
     {
         Schema::create('posts', function (Blueprint $table) {
             $table->id();
-            $table->integer('user_id')->unsigned();
             $table->string('title');
             $table->text('content');
             $table->timestamps();
         });
     }
```
- On `Photo.php` model
```diff
class Photo extends Model
{
     use HasFactory;

+    public function imageable()
+    {
+        return $this->morphTo();
+    }

}
```
- On `Post.php`,`User.php` model
```diff
         return $this->belongsTo('App\Models\User');
     }

+    public function photos()
+    {
+        return $this->morphMany('App\Models\Photo', 'imageable');
+    }
```

## Many-to-Many Polymorphic Relation
- Share a single list of unique records among the rest of the tables
- `php artisan make:model Video -m` Creating a table named `Video`
- `php artisan make:model Tag -m` Creating a table named `Tag`
- `php artisan make:model Taggable -m` Creating a table named `Taggable`
- `Videos` migration
```diff
     public function up(): void
     {
         Schema::create('videos', function (Blueprint $table) {
             $table->id();
+            $table->string('name');
             $table->timestamps();
         });
     }
```
- `Tag` migration
```diff
     public function up(): void
     {
         Schema::create('videos', function (Blueprint $table) {
             $table->id();
+            $table->string('name');
             $table->timestamps();
         });
     }
```
- `Taggable` migration
```diff
     public function up(): void
     {
         Schema::create('taggables', function (Blueprint $table) {
-            // $table->id();
+            $table->integer('tag_id');
+            $table->integer('taggable_id');
+            $table->integer('taggable_type');
-            // $table->timestamps();
         });
     }
```
- `Post.php` model
```php
    public function tags()
    {
        return $this->morphToMany('\App\Models\Tag', 'taggable');
    }
```
- `Tag.php` model
```php
    public function posts()
    {
        return $this->morphByMany('App\Models\Post', 'taggable');
    }

    public function videos()
    {
        return $this->morphByMany('App\Models\Video', 'taggable');
    }

```

## Retrieving data - Polymorphic relation many-to-many
- [Code commit 1](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/0e6f101ce66db9f5a9aa298698378e677eaacc6c) [Code commit 2](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/739257353314d31ebc7cf91c5a13834961375557)
