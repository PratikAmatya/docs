+++
title = 'LEMP Stack'
date = 2023-11-27T12:25:32+05:45
draft = false
+++

### Set locale

In `/etc/default/locale`, set the following

```bash
sudo nano /etc/default/locale
```

```bash
LANG=en_US.UTF-8
LANGUAGE=en_US.UTF-8
LC_ALL=en_US.UTF-8
```

---

### Update apt-get

```bash
$ sudo apt-get update
```

---

### Install Nginx

```bash
$ sudo apt-get install nginx
```

#### Try http://ip-address to see if nginx loads properly

---

### Install MySQL Server

```bash
$ sudo apt-get install mysql-server
```

---

### Install PHP

**Check which version is being installed. The version is required later.**

```bash
$ sudo apt-get install php-fpm php-mysql
```

---

### Install phpmyadmin

```bash
$ sudo apt-get install phpmyadmin
```

1. Do not select any in the first selection for server as we have already installed Nginx
2. In the second option, SELECT yes
3. You will be asked to set password for the database
4. Simply, add password and select enter

---

### Create _symlink_ of phpmyadmin with

**Symlink = Shortcut**

```bash
$ sudo ln -s /usr/share/phpmyadmin /var/www/html
```

---

**NOTE: Change nginx sites-available for php and phpmyadmin**

```bash
sudo nano /etc/nginx/sites-available/default
```

> Uncomment the following lines
>
> Do not forget to uncomment the last curly bracket
>
> Make sure the PHP version matches the installed version
>
> Usually it is _8.1_

```
 location ~ \.php${
 include snippets/fastcgi-php.conf
 fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
 }
```

### Test the file configuration

```bash
sudo nginx -t
```

### Reloading the Nginx with given changes

```bash
sudo service nginx reload
```

---

### Create New User for phpmyadmin

```bash
sudo mysql --user=root mysql
```

```mysql
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'some_pass';
```

> For connecting to the database from other server, use % when creating the user

```mysql
CREATE USER 'admin'@'%' IDENTIFIED BY 'some_pass'
```

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;
```

```mysql
FLUSH PRIVILEGES;
```

---

### Create swap file

[Digitalocean Tutorial](https://www.digitalocean.com/community/tutorials/how-to-configure-virtual-memory-swap-file-on-a-vps#4)

> Swap file allows the use of hard disk memory to be used as RAM

Check if swap exists with

```bash
free

```

Create swapfile with

```bash
cd /var
sudo touch swap.img
sudo chmod 600 swap.img
sudo dd if=/dev/zero of=/var/swap.img bs=1024k count=1000
sudo mkswap /var/swap.img
sudo swapon /var/swap.img
```

---

### Install Nodejs

```bash
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
```

```bash
sudo apt-get install -y nodejs
```

---

### Install PM2

```bash
sudo npm install pm2@latest -g
```

---

### Start API using pm2

> Here, name parameter is optional

```bash
pm2 start app.js --name API
```
