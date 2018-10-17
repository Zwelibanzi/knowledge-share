run `composer install`

[Optional] Run `php bin/console list` to see which commands you have access to. These include: `make`, `server` and `doctrine:fixtures`

Run `php bin/console server:start` to bring up symfony server, then navigate to the provided URL

#MAKE AN NGINX SERVER BLOCK

 - stop symfony server by running `php bin/console server:stop`
 - copy `nginx.conf.dist` file to `/etc/nginx/sites-available/` and edit it to cater for your local environment
 - create symbolic link by running `sudo ln -s /etc/nginx/sites-available/YOUR_CONFIG_FILE_NAME /etc/nginx/sites-enabled/`
 - update your `/etc/hosts` file with the specified server name from your `nginx` configuration file
 - restart nginx by running: `sudo service nginx restart`
 - navigate to your server name with http:// appended on the URL

#DATABASE SETUP
   - Run this command to install mysql: `sudo apt install mysql-server` 
   - Change the password to something you can remember:   
    - Run this command to view mysql user information: `SELECT user,authentication_string,plugin,host FROM mysql.user;`
    - Run this command to change root password: `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YOUR_CHOSEN_PASSWORD'`;
    - Run this command to get the server to put your new changes into effect: `FLUSH PRIVILEGES;`

#START BUILDING THE APP!
Create an Entity:   
- `php bin/console make:entity`

Create Form for the entity:
 - `php bin/console make:form`

#CREATE DATABASE:
- inside `.env` replace the database default parameters with the ones from your environment

Synchronise your database with your entities
 - `php bin/console doctrine:schema:update --force`

Create dummy data using doctrine fixture
 - `php bin/console make:fixtures`

Synchronise the data with what the fixture is doing 
 - `php bin/console doctrine:fixtures:load`
