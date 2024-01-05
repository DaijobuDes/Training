# Database - Artisan Tinker
- Interacts to the database using the Eloquent API

## Using tinker
- Command: `php artisan tinker`
- An interactive console, can create, read, update or delete data via the command line.
- Still uses PHP code and the Eloquent API in order to interact with the database.
- Creating data
```php
use App\Models\Post;

Post::create(['title'=>'Some PHP title here created by tinker','content'=>'Another or some content here']);

$post = new Post;
$post->title = "Assigning \$post->title to some text string here";
$post->content = "Some more content here";
$post->save;

```
- Reading data
```php
use App\Models\Post;

Post::find(1);
Post::find(2);
Post::where('id', 3)->first();
Post::whereId(4)->first();
Post::all();


```
- Updating data
```php
use App\Models\Post;

$post = Post::find(4);
$post->title = "updated title";
$post->content = "updated content";
$post->save();


```
- Deleting data
```php
use App\Models\Post;

// Soft delete
$post = Post::find(8);
$post->delete();

Post::find(8)->delete();

// Retrieve soft deleted items
Post::onlyTrashed()->get();

// Permanently delete soft deleted items
Post::onlyTrashed()->forceDelete();

$post = Post::onlyTrashed();
$post->forceDelete();

```
