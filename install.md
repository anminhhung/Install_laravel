## Step 0 — update your system, Install prerequisites
    sudo apt update

* Before anything you should install git, curl, wget, … in a fresh ubuntu 18.04:
    sudo apt install -y git curl wget zip unzip

## Step 1 — Install Apache:
    sudo apt install apache2

* To make sure that the server is running check the apache2 status:
    sudo systemctl status apache2

and then press “q” to quit this session.

## Step 2 — Adjust the Firewall to Allow Web Traffic
sudo ufw allow in "Apache Full"

* Then check this address in the browser : http://your_server_ip 
    exp: http://127.0.0.1

* Attention: Enabling mod_rewrite
    sudo a2enmod rewrite
    sudo systemctl restart apache2

## Step 3— Install MySQL:
    sudo apt install mysql-server

* Then remove some dangerous defaults after installing mysql:
    sudo mysql_secure_installation

* Think about a strong password for user root in Mysql ( in level 1=Medium, it must have sing, digit, lowercase and uppercase letters). Don’t forget to save it.

* And then answer the other questions arise with Yes!
    Remove anonymous users? y
    Disallow root login remotely? y
    Remove test database and access to it? y
    Reload privilege tables now? y

* Try to connect mysql with root password
    sudo mysql -u root -p

## Step 4— Install PHP:
    sudo apt install php libapache2-mod-php php-mysql

* For Laravel installation and also phpmyadmin you will need some important php modules, so do this:
    sudo apt install php7.2-common php7.2-cli php7.2-gd php7.2-mysql php7.2-curl php7.2-intl php7.2-mbstring php7.2-bcmath php7.2-imap php7.2-xml php7.2-zip

## Step 5— Tell the web server to prefer PHP files over others, so make Apache look for an index.php file first.
    sudo nano /etc/apache2/mods-enabled/dir.conf

* Then edit the dir.conf file in a way that index.php has the priority over the others, as like as:
    <IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
    </IfModule>

* Then Ctrl+x and answer yes to override the file. Then
    sudo systemctl restart apache2

* Check the correctness of installation by:
    sudo nano /var/www/html/info.php

* And put this:
    <?php
        phpinfo();
    ?>

* Then check in the browser this: http://your_server_ip/info.php
    exp: http://127.0.0.1/info.php

## Step 6— Install composer on Ubuntu
    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer
    
    sudo chmod +x /usr/local/bin/composer

    composer --version

## Step 7 — Install Fresh Laravel Project on Ubuntu
    cd ~
    composer create-project --prefer-dist laravel/laravel DIR_NAME(name folder want to create)

* Then go to the project directory :
    cd DIR_NAME
* and then start the project:
    php artisan serve
