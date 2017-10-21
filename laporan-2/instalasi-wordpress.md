# Instalasi WordPress Pada Ubuntu 16.04
## Sumber
1. Instalasi Linux, Apache, MySQL, PHP (LAMP) Stack pada Ubuntu 16.04 (https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04)
2. Instalasi WordPress 4.7 pada Ubuntu 16.10/16.04 menggunakan LAMP Stack (https://www.tecmint.com/install-wordpress-on-ubuntu-16-04-with-lamp/)

## Langkah-langkah Menginstall WordPress Pada Ubuntu 16.04
1. Update terlebih dahulu`sudo apt-get update`
2. Install Apache `sudo apt-get install apache2`
3. Konfigurasi pada apache2.conf dan tambahkan ServerName `sudo nano /etc/apache2/apache2.conf`
![](/assets/wordpress/1_1.png)
4. Lakukan pengecekan syntax `sudo apache2ctl configtest`
5. Setelah melakukan perubahan, restart Aoache `sudo systemctl restart apache2`
![](/assets/wordpress/2.png)
6. Inisiasi aktivasi UFW firewall `sudo ufw app list` `sudo ufw app info "Apache Full"` `sudo ufw allow in "Apache Full"`


