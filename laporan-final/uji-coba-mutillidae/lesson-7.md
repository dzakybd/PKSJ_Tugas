Lesson 7 - SQL Injection, Burpsuite, cURL, Perl Parser
-------

### # Mempersiapkan Burp Suite dan Firefox

- **Step 1** : Buka halaman user info. Pilih sidebar. OWASP Top 10 --> A1 - SQL Injection --> SQLi - Extract Data --> User Info
![](/assets/lesson-7/VirtualBox_kali_19_12_2017_03_01_34.png)


-  **Step 2** : Setting proxy pada firefox dengan membuka pengaturan network melalui open menu --> Preferences -> Advanced --> Network

- **Step 3** : Pada bagian connection, klik tombol _Settings_. Setelah mengklik tombol _Settings_, maka akan muncul kotak dialog _Connection Settings_. Atur _Connection Settings_ sesuai gambar.

![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_06_35.png)

- **Step 4** : Buka burpsuite, dengan cara pilih Applications --> Web Application Analysis --> burpsuite

![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_10_12.png)


 - **Step 5** : Pada saat burpsuite telah dibuka, maka akan ditanyakan tentang project. Klik tombol Next 
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_24_51.png)
 
 - **Step 6** : Setelah menekan tombol next, maka selanjutnya ada memilih konfigurasi burp. Pilih radio button User Burp defaults dan Klik Start Burp
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_26_28.png)
 
 - **Step 7** : Setelah menekan tombol Start Burp, maka aplikasi Burp Suite sudah berjalan. Langkah selanjutnya adalah memastikan apakah port proxy pada Burp Suite adalah 8080, dengan cara memilih menu Proxy --> Options
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_31_58.png)
 
 - **Step 8** : Setelah memastikan port porxy 8080, maka selanjutnya adalah mematikan Intercept pada menu Proxy --> Intercept.
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_34_07.png)
 
 
 ### # SQL Injection: Obtain Userlist (Method #1)
 - **Step 1** : Buka halaman user info. Pilih sidebar. OWASP Top 10 --> A1 - SQL Injection --> SQLi - Extract Data --> User Info
 - **Step 2** : Melakukan SQL Injection untuk mendapatkan semua user tanpa password dengan cara memasukkan `' or 1=1--` pada kolom username. Kemudian tekan tombol _View Account Detail_.
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_51_37.png)
 
 - **Step 3** : Setelah menekan tombol _View Account Detail_, maka halaman akan muncul error query. Perhatikan syntax query yang digunakan. 
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_42_33.png)
 
 - **Step 4** : Setelah melihat syntax query yang digunakan bahwa syntax comment `--` untuk sql tidak berjalan karena kurang spasi. Maka selanjutnya adalah menambahkan spasi setelah tanda comment sql `--` menjadi `' or 1=1-- `. Kemudian tekan tombol _View Account Detail_ lagi.
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_52_52.png)
 
 
 - **Step 5** : Maka hasilnya kita mendapatkan data user.
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_16_55_56.png)
 
 - **Step 6** : Buka Burp Suite kemudian pilih menu Proxy -> HTTP History. Kemudian cari log hasil sniffing **step 5**. Perhatikan header requestnya.
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_17_03_16.png)
 
 
 #### # Simulate CURL SQL Injection: (Method #2)
 - **Step 1** : Copy cookies PHPSESSID pada header request pada Burp Suite Bagian SQL Injection: Obtain Userlist (Method #1) **Step 6** dan simpan pada file crack_cookies.txt
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_17_49_09.png)
 - **Step 2** : Jalankan perintah
 
 `curl -b crack_cookies.txt -c crack_cookies.txt --user-agent "Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)" --data "page=user-info.php&username=%27+or+1%3D1--+&password=&user-info-php-submit-button=View+Account+Details" --location "http://10.151.36.64/mutillidae/index.php" | grep -i "Username=" | awk 'BEGIN{FS="<"}{for (i=1; i<=NF; i++) print $i}' | awk -F\> '{print $2}'`
 
 - **Step 3** : Setelah menjalankan perintah, hasil dari curl sql injection dapat dilihat pada terminal.
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_17_57_09.png)
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_18_03_41.png)
 
#### # Perl Parser

 - **Step 1** : Download perl parser lesson 7 pada link berikut [http://www.computersecuritystudent.com/SECURITY_TOOLS/MUTILLIDAE/MUTILLIDAE_2511/lesson7/lesson7.pl.TXT](http://www.computersecuritystudent.com/SECURITY_TOOLS/MUTILLIDAE/MUTILLIDAE_2511/lesson7/lesson7.pl.TXT)
 
 - **Step 2** : Ganti nama file lesson7.pl.TXT menjadi lesson7.pl, kemudian ubah permission file tersebut menjadi `rwx------` atau 700.
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_18_08_20.png)

 - **Step 3** : Jalankan perintah 
 `curl -b crack_cookies.txt -c crack_cookies.txt --user-agent "Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)" --data "page=user-info.php&username=%27+or+1%3D1--+&password=&user-info-php-submit-button=View+Account+Details" --location "http://10.151.36.64/mutillidae/index.php" | grep "Username=" > lesson7.txt`. Perintah tersebut akan menyimpan hasil curl pada file lesson7.txt
 
 ![](/assets/lesson-7/VirtualBox_kali_19_12_2017_18_11_36.png)
 
 **Step 4** : Jalankan lesson7.pl dan kemudian lihat hasilnya.
 
 
 
 
 
 


