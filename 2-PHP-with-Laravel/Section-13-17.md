# Eloquent Relationships CRUD
- [Repository Branch Commits (Step by Step as seen on the Videos)](https://github.com/kateaubreycellan-nabepero/eloquent-crud/branches/)


## Eloquent One-to-One Relationship CRUD
- [Branch Commits](https://github.com/kateaubreycellan-nabepero/eloquent-crud/commits/eloquent-one-to-one)
- `php artisan make:model Address -m`

## Eloquent One-to-Many Relationship CRUD
- [Branch Commits](https://github.com/kateaubreycellan-nabepero/eloquent-crud/commits/eloquent-one-to-many)
- `php artisan make:model Post -m`

## Eloquent Many-to-Many Relationship CRUD
- [Branch Commits](https://github.com/kateaubreycellan-nabepero/eloquent-crud/commits/eloquent-many-to-many)
- `php artisan make:model Role -m`
- `php artisan make:migration create_role_user_table --create=role_user`

## Eloquent Polymorphic Relationship CRUD
- [Branch Commits](https://github.com/kateaubreycellan-nabepero/eloquent-crud/commits/eloquent-polymorphic)
- `php artisan make:model Staff -m`
- `php artisan make:model Product -m`
- `php artisan make:model Photo -m`

## Eloquent Polymorphic Many-to-Many Relationship CRUD
- [Branch Commits](https://github.com/kateaubreycellan-nabepero/eloquent-crud/commits/eloquent-polymorphic-many-to-many)
- `php artisan make:model Post -m`
- `php artisan make:model Video -m`
- `php artisan make:model Tag -m`
- `php artisan make:model Taggable -m`