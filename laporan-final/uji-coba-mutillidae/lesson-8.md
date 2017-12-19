Lesson 8 - SQL Injection Union Exploit #1
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
 
 
### # SQL Injection (Union Example #1)
 
 - **Step 1** : Buka halaman user info. Pilih sidebar. OWASP Top 10 --> A1 - SQL Injection --> SQLi - Extract Data --> User Info
![](/assets/lesson-7/VirtualBox_kali_19_12_2017_03_01_34.png)


- **Step 2** : Ubah ukuran text box username menjadi 100% menggunakan inspect element agar text box lebih panjang untuk menuliskan syntax SQL Injection.
![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_37_43.png)

- **Step 3** : Masukkan syntax sql `' union select null -- ` pada text box name untuk perbocaan pertama melakukan sql injection dan tekan tombol _View Account Details_.
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_40_50.png)
 