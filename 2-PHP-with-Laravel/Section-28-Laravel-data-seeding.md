# Laravel data seeding
- Creating a seeder for a table, `php artisan make:seeder <name>`
- Edit the newly created php file for seeding using raw SQL
- Call the class using `$this->call(UsersTableSeeder::class);`
- Begin seeding by `php artisan db:seed`
- One can also create advanced seeding methods by factories
- The faker library generates data almost like a legitimate data