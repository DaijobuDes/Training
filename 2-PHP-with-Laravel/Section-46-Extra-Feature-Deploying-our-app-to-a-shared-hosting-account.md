# Laravel Extra Features (Deploying Our App to a Shared Hosting Account)
- On the lecture, they are using GoDaddy to host
- On the latest versions windows 10, SSH binaries are included by default and can be ran through the command prompt by `ssh username@hostname`
- Once logged in, on some servers, PHP needs to be manually installed, and some of its modules
- Once PHP is installed, one can install composer and laravel the normal way.
- Transferring the files have a lot of ways, either via SCP, SFTP, cloning a git repository and more.
- Once transferred, configure `.env` with the correct options and migrate the database
