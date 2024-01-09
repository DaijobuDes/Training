# Middleware - Security / Protection
- Creating a middleware: `php artisan make:middleware RoleMiddleware`
- Maintenance mode: `php artisan down`
- Reverting maintenenace mode: `php artisan up`

## More practical ways to use middlewares
### 1. Setup phase
- First create role table with migration `php artisan make:model Role -m`
- Edit migrations with role_id and role_name
- Refresh and migrate the database

### 2-4. Custom methods
- Creating custom methods inside the middleware
- `php artisan make:controller AdminController`

## Branch commits
- Registering the new middleware - [dfac9fff3f9c21c5e822312d6fcda897dd54538b](https://github.com/kateaubreycellan-nabepero/forms-demo/commit/dfac9fff3f9c21c5e822312d6fcda897dd54538b)

- Basic usage of middleware - [fec7aefd245ca682cbca5bbd19dd9596c9a61968](https://github.com/kateaubreycellan-nabepero/forms-demo/commit/fec7aefd245ca682cbca5bbd19dd9596c9a61968)

- Middleware: Migrations and relations setup - [7a44b0b351a8461294bf8553dc18ddce07ac55a0](https://github.com/kateaubreycellan-nabepero/forms-demo/commit/7a44b0b351a8461294bf8553dc18ddce07ac55a0)

- Middleware: Custom methods and identifying user role - [a43adf0ba93b5ef30b3e3c5f1249efd10fdc5524](https://github.com/kateaubreycellan-nabepero/forms-demo/commit/a43adf0ba93b5ef30b3e3c5f1249efd10fdc5524)

- Middleware: Creating a new controller - [95eba72fd7b0a1255dd70f1b94607d0ef30c9a48](https://github.com/kateaubreycellan-nabepero/forms-demo/commit/95eba72fd7b0a1255dd70f1b94607d0ef30c9a48)

- Middleware: Accessing admin/user page with redirects - [2a28cebf43891c12c23c87f2052b23f5e7aaa9d6](https://github.com/kateaubreycellan-nabepero/forms-demo/commit/2a28cebf43891c12c23c87f2052b23f5e7aaa9d6)