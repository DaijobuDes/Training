# New Application - Laravel 7 - Permissions and Roles - CRUD
- Methods used discussed on the previous sections
- Creating a page for the roles and permissions for the admin user
- Front-end side is list all the available roles, edit role name, create a role or delete role.
- Checking unchanged values by using `isDirty()` returns true if the value is unchanged when updating records
- `isClean()` returns true if the value has been changed when updating records
- Protecting a route locally, editing the routes file is an option and using `Route::middleware()` and placing the route and its groups.
- Protecting a route globally, editing the route service provider and placing the middleware groups.