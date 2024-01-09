# Database - Laravel Migrations

## Environment configurations
- In laravel projects, there is an `.env` file in where all sensitive information is store like the database usernaame and password, some keys and etc.
- `.env` is automatically ignored via `.gitignore` when generating the base files for the project
- An example of the `.env` file is found by the name `.env.example` file

## Windows OS Migrations
- Laravel manages the tables, migration files are found under `./database/migrations/` folder
- Access SQL and create a new database, e.g `CREATE DATABASE new_cms;`
- Then go to the project folder and edit `.env` file with the correct database name, username and password
- After editing, run `php artisan migrate` to create tables.
- More methods of creating columns on the table are **[found here](https://laravel.com/docs/10.x/migrations#available-column-types)**


## Creating migrations from scratch
- `php artisan make:migration create_posts_table --create="posts"`
-  Syntax: `php artisan command migration_name --create="table_name"`
- This creates a new migration file under `./database/migrations/` folder.
- Editing the `up()` method adds columns to the table while `down()` drops the table
- To rollback/delete the new table created without resetting, enter `php artisan migrate:rollback`
- One can change the column name but will apply once the user has applied the migration command

## Adding columns to existing tables using migrations
- `php artisan make:migration add_is_admin_column_to_posts_table --table="posts"`
- `--table="posts"` refers to the table **"posts"**
- On adding a column
```diff
     public function up(): void
     {
        Schema::table('posts', function (Blueprint $table) {
+            $table->integer('is_admin')->unsigned();
         });
     }
```
- On removing a column
```diff
     public function down(): void
     {
         Schema::table('posts', function (Blueprint $table) {
+            $table->drop('is_admin');
         });
     }
```
- Rollback: `php artisan migrate:rollback`
- Apply: `php artisan migrate`

## More migration commands
| Command               | Description
------------------------|---------------------------------------------------
| `migrate:fresh` | Drop all tables and re-run all migrations
| `migrate:install` |Create the migration repository
| `migrate:refresh` | Reset and re-run all migrations
| `migrate:reset` | Rollback all database migrations
| `migrate:rollback` | Rollback the last database migration
| `migrate:status` | Show the status of each migration
