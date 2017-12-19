Lesson 7 - SQL Injection, Burpsuite, cURL, Perl Parser
-------

### # Mempersiapkan Burp Suite dan Firefox

- **Step 1** : Buka halaman user info. Pilih sidebar. OWASP Top 10 --> A1 - SQL Injection --> SQLi - Extract Data --> User Info
![](/assets/VirtualBox_kali_19_12_2017_03_01_34.png)


-  **Step 2** : Setting proxy pada firefox dengan membuka pengaturan network melalui open menu --> Preferences -> Advanced --> Network

- **Step 3** : Pada bagian connection, klik tombol _Settings_. Setelah mengklik tombol _Settings_, maka akan muncul kotak dialog _Connection Settings_. Atur _Connection Settings_ sesuai gambar.

![](/assets/VirtualBox_kali_19_12_2017_16_06_35.png)

- **Step 4** : Buka burpsuite, dengan cara pilih Applications --> Web Application Analysis --> burpsuite

![](/assets/VirtualBox_kali_19_12_2017_16_10_12.png)


 - **Step 5** : Pada saat burpsuite telah dibuka, maka akan ditanyakan tentang project. Klik tombol Next 
 
 ![](/assets/VirtualBox_kali_19_12_2017_16_24_51.png)
 
 - **Step 6** : Setelah menekan tombol next, maka selanjutnya ada memilih konfigurasi burp. Pilih radio button User Burp defaults dan Klik Start Burp
 
 ![](/assets/VirtualBox_kali_19_12_2017_16_26_28.png)
 
 - **Step 7** : Setelah menekan tombol Start Burp, maka aplikasi Burp Suite sudah berjalan. Langkah selanjutnya adalah memastikan apakah port proxy pada Burp Suite adalah 8080, dengan cara memilih menu Proxy --> Options
 
 ![](/assets/VirtualBox_kali_19_12_2017_16_31_58.png)
 
 - **Step 8** : Setelah memastikan port porxy 8080, maka selanjutnya adalah mematikan Intercept pada menu Proxy --> Intercept.
 
 ![](/assets/VirtualBox_kali_19_12_2017_16_34_07.png)
 
 
 ### # SQL Injection: Obtain Userlist (Method #1)
 - **Step 1** : Buka halaman user info. Pilih sidebar. OWASP Top 10 --> A1 - SQL Injection --> SQLi - Extract Data --> User Info
 - **Step 2** : Melakukan SQL Injection untuk mendapatkan semua user tanpa password dengan cara memasukkan `' or 1=1--` pada kolom username
 


