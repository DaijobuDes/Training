# New application - Laravel 7 roles and permissions - Mirgrations and relationships
- Already discussed in the previous videos but using Laravel 7
- Editing front-end side for the admin user
- Separating routes, especially for large applications, on the `web.php` to other files and editing the route service provider to let it point to the multiple routes file.
- Assigning the proper permissions of the pages which can be only accessible to the admin and the user to view the profile of their own, while the admin can view any user's profile using middleware.