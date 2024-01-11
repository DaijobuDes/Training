# New application - Laravel 7
- A review on past sections on how to basics on laravel condensed into a single section using Laravel 7
- On the previous lessons, the video was not using foreign keys.
- They can be chained like `$table->foreignId('column')->references('column')->on('table')->onDelete('cascade');`
- Some methods were removed/deprecated from version 5 to version 7
- Introduced laravel policies, they can be created via artisan
- `php artisan make:policy PostPolicy --model=Post`
- File can be found under `./app/Policies/` folder