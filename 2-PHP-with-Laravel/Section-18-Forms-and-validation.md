# Forms and Validation (branch commits)
Restore user_id on Post table - [05105fa0c8bbadd962c2135bbcb44d550d8716c2](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/05105fa0c8bbadd962c2135bbcb44d550d8716c2)

Routes cleanup - [e9802b7ba7ec3ea1c58cc7cca3d522692f5114fd](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/e9802b7ba7ec3ea1c58cc7cca3d522692f5114fd)

Setting up views and routes - [8b11389d19bf6b62cb2638ae134a133261da3571](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/8b11389d19bf6b62cb2638ae134a133261da3571)

Setting up the markup for create - [bc396263e25e9f61d37c2f4dfc2788d092dbc670](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/bc396263e25e9f61d37c2f4dfc2788d092dbc670)

Controller and view setup - [8a345ec62cc5f61c545a121a4e4efd4aa2535317](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/8a345ec62cc5f61c545a121a4e4efd4aa2535317)

Persisting data to database - [874600d4f3711e024220390bba4891dccf66d368](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/874600d4f3711e024220390bba4891dccf66d368)

Reading data - [e97117003ce062ec7fb5a64b619b3a6ca456abed](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/e97117003ce062ec7fb5a64b619b3a6ca456abed)

Showing individual posts and updating them - [3bd096d02e72ee28501071e4d37179c2e8c35f37](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/3bd096d02e72ee28501071e4d37179c2e8c35f37)

Deleting data - [ee576f3dec994bc7d484159df2b9c0bb283a6404](https://github.com/kateaubreycellan-nabepero/laravel-test-and-demo/commit/ee576f3dec994bc7d484159df2b9c0bb283a6404)

## Commands to replicate models
- `php artisan make:model Post -m`
- `php artisan make:migration add_is_admin_column_to_posts_table --table="posts"`
- `php artisan make:migration add_deleted_at_column_to_posts_table --table="posts"`
- `php artisan make:model Role -m`
- `php artisan make:migration create_role_user_table --create=role_user`
- `php artisan make:model Country -m`
- `php artisan make:migration add_country_id_column_to_users --table=users`
- `php artisan make:model Photo -m`
- `php artisan make:model Video -m`
- `php artisan make:model Tag -m`
- `php artisan make:model Taggable -m`
