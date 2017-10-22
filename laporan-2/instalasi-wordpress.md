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
7. Cek IP jika server sudah terinstall
![](/assets/wordpress/3.png)
8. Instalasi PHP `sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql`
9. Ubah urutan ekstensi php `sudo nano /etc/apache2/mods-enabled/dir.conf`
![](/assets/wordpress/4.png)
10. Restart Apache `sudo systemctl restart apache2`
11. Cek jika PHP sudah terinstall dengan membuat file di `sudo nano /var/www/html/info.php`
12. Tambahkan kodingan `<?php phpinfo(); ?>`
13. Cek IP maka akan muncul halaman php
![](/assets/wordpress/7.png)
14. Masuk ke command-line dari MySQL `mysql -u root -p`
15. Buat database baru `CREATE DATABASE wordpress;`
16. Buat user dan password baru `CREATE USER wordpressuser@localhost IDENTIFIED BY 'password';`
17. Tambahkan permission untuk user baru `GRANT ALL PRIVILEGES ON wordpress.* TO wordpressuser@localhost;`
18. Flush data dengan `FLUSH PRIVILEGES;` kemudian keluar dari command line `exit`
19. Download WordPress `wget http://wordpress.org/latest.tar.gz`
20. Ekstrak hasil download `tar xzvf latest.tar.gz`
21. Buka folder WordPress `cd ~/wordpress`
22. Copy file `cp wp-config-sample.php wp-config.php` dan buka filenya `nano wp-config.php`
23. Definisikan database
![](/assets/wordpress/12.png)
24. Amankan WordPress `curl -s https://api.wordpress.org/secret-key/1.1/salt/`
25. Masuk ke Halama html `cd /var/www/html`
26. Buat ownership yang baru `sudo chown -R demo:www-data *`
27. Buka IP untuk konfigurasi WordPress
![](/assets/wordpress/13.png)

