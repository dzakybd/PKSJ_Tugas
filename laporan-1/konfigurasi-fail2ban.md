## Konfigurasi Fail2Ban
#### Requirement
- install fail2ban

#### Konfigurasi Fail2Ban
* **Step 1** : Instalasi melalui package manager apt dengan perintah

 `sudo apt-get install fail2ban `
 
 ![](/assets/fail2ban/1.PNG)
 
* **Step 2** : Tunggu sampai proses instalasi selesai. Kemudian buka file **jail.conf** yang berada pada folder **/etc/fail2ban**

 ![](/assets/fail2ban/3.PNG)
 
* **Step 3** : Atur beberapa variabel konfigurasi. Ubah maxretry menjadi 3 yang semula adalah 5. Untuh mencegah percobaan serangan.

 ![](/assets/fail2ban/4.1.PNG)
 
* **Step 4** : Restart fail2ban dengan perintah

  `sudo service fail2ban restart`
  
  ![](/assets/fail2ban/5.PNG)
  
* **Step 5** : Cek apakah fail2ban sudah terinstall dengan sempurna dengan menjalankan perintah
  
  `sudo iptables -S`
   
   ![](/assets/fail2ban/6.PNG)
   
   
   
Sumber : [How To Protect SSH with Fail2Ban on Ubuntu 14.04 - DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04)

 