
## How To Setup Configure **Digitalocean** Hosting Server For **Laravel** 
After Create Droplet Server on Digital Ocean . 
#### 1 - Login To Your server using shell. 

- `ssh root@ip_address`
#### 2- install PHP and extensions required to LARAVEL 
- `apt-get update && apt-get upgrade`
- `add-apt-repository ppa:ondrej/php `
- `apt-get update`
- `apt-get install php7.4 `
- `apt-get install php-pear php7.4-curl php7.4-dev`
- `apt-get install php7.4-gd php7.4-mbstring php7.4-zip`
- `apt-get install php7.4-mysql php7.4-xml`

#### 3- Install MYSQL Server 
- Update apt : `sudo apt update`
- install mysql-server package : `sudo apt install mysql-server`

#### 4- Configuring MySQL 
- `sudo mysql `
- `ALTER USER ‘root’@’localhost’ IDENTIFIED WITH mysql_native_password BY 'set_password'; `
- After that `exit;`
- Restart MySQL : `sudo service mysql start`
- After Restart Check Your Connection in Database : ` systemctl status mysql.service`
- After that , lets start to make DATABASE
- `sudo mysql` or  `sudo mysql -u root -p `
- `create database name_database;`
- For Show All Databases`SHOW DATABASES;`

#### 5- Install Laravel From git using shell 
- `apt install composer`
- `cd /var/www`
- `git clone repo_project`
- `cd repo_project`
- `composer install`
- Change Name File .env.example to .env : `cp .env.example .env`
- Login to file **.env** and update value for *APP_URL & db_name & username & db_password* `vim .env `
- After that close file and save config `ESC SHIFT + :wq` and `enter`
- Migrate table in your project and create key  `php artisan migrate` & `php artisan key:generate`

#### 6- Setup Apache Configuration
- After Login To ssh : `cd /etc/apache2/sites-available`
- `sudo vim 000-default.conf`
- **Are you ready now to adjust your project files with the server ?**

```` console
<VirtualHost*:80>
ServerAdmin webmaster@localhost
DocumentRoot/var/www/your_repo/public
<Directory/var/www/your_repo/public>
Options Indexes FollowSymLinks
AllowOverride All
Require all granted
</Directory>
ErrorLog$(APACHE_LOG_DIR)/error.log
CustomLog$(APACHE_LOG_DIR)/access.log combined
<IfModule mod_dir.c>
DirectoryIndex index.php index.pl index.cgi index.html index.xhtml index.htm
</IfModule>
</VirtualHost>

````
- After that close file and save config `ESC SHIFT + :wq` and `enter`
- Restart Apache `sudo a2enmod rewrite`
- `systemctl restart apache2` **OR** `sudo service apache2 restart`
- issues you are expected to encounter : 

  - `cd /var/www/your_project`
  - `sudo chmod -R 777 storage`
  - `sudo chmod -R 777 public` 
