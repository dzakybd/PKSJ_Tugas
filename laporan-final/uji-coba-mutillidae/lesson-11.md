Lesson 11 - SQL Injection Union Exploit #4
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
 
 
<<<<<<< HEAD
=======
<<<<<<< HEAD
### # SQL Injection (Union Example #1)
 
 - **Step 1** : Buka halaman user info. Pilih sidebar. OWASP Top 10 --> A1 - SQL Injection --> SQLi - Extract Data --> User Info
![](/assets/lesson-7/VirtualBox_kali_19_12_2017_03_01_34.png)


- **Step 2** : Ubah ukuran text box username menjadi 100% menggunakan inspect element agar text box lebih panjang untuk menuliskan syntax SQL Injection.
![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_37_43.png)

- **Step 3** : Masukkan syntax sql `' union select null -- ` pada text box name untuk perbocaan pertama melakukan sql injection dan tekan tombol _View Account Details_.
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_40_50.png)
 
- **Step 4** : Setelah menekan tombol _View Account Details_, maka akan terjadi error query karena jumlah kolom dan kolom union berbeda.
![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_44_12.png)

- **Step 5** : Lakukan **Step 2** kembali. Setelah melakukan **Step 2**, lakukan kembali **Step 3** dengan menambah `null` pada syntax query sql injection. Contoh penambahan `null` pada query sql injection `' union select null,null -- `.

- **Step 6** :  Lakukan **Step 5** sampai jumlah kolom union dan kolom table accounts sama. `' union select null,null,null,null,null -- ` adalah syntax query hasil percobaan **Step 5**. Dapat disimpulkan jumlah kolom pada table accounts adalah 5.

- **Step 7** : Masukkan query sql injection `' union select null,null,null,null,null -- ` pada textbox name. Dan kemudian tekan tombol _View Account Details_.
![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_56_23.png)

- **Step 8** : Setelah menekan tombol _View Account Details_, maka hasilnya akan menunjukan kolom yang ditampilkan pada web.
![](/assets/lesson-8/VirtualBox_kali_19_12_2017_20_58_23.png)

- **Step 9** : Lakukan **Step 7** kembali dengan mengganti `null` menjadi angka dengan query sql injection sebagai berikut `' union select 1,2,3,4,5 -- `
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_03_20.png)
 
- **Step 10** : Dapat dilihat dari hasil percobaan **Step 9** bahwa kolom username diisi oleh nomer 2, password diisi oleh nomer 3 dan Signature diisi oleh nomer 4.
 
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_04_19.png)

- **Step 11** : Langkah selanjutnya adalah melakukan serangan sql injection dengan menggabungkan dengan tabel yang sudah diketahui selain accounts. Contohnya menggunakan tabel credit_cards, sehingga query sql injectionnya menjadi `' union select ccid,ccnumber,ccv,expiration,null from credit_cards -- `
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_10_49.png)
 
- **Step 12** : Maka hasilnya, bagian username diisi oleh ccnnumber, password diisi oleh ccv, dan signature diisi oleh expiration. 
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_12_04.png)
 

### # Curl Action
- **Step 1** : Buka Burp Suite dan cari log hasil sniffing pada **step 12** pada bagian SQL Injection (Union Example #1), kemudian catat/copas raw header request.
![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_17_58.png)

- **Step 2** : Copas Cookie pada hasil header dan masukkan pada file crack_cookies.txt
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_21_02.png)
 
- **Step 3** : Jalankan perintah 
`curl -b crack_cookies.txt -c crack_cookies.txt --user-agent "Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)" --data "page=user-info.php&username=%27+union+select+ccid%2Cccnumber%2Cccv%2Cexpiration%2Cnull+from+credit_cards+--+&password=&user-info-php-submit-button=View+Account+Details" --location "http://10.151.36.64/mutillidae/index.php" | grep -i "Username=" | awk 'BEGIN{FS="<"}{for (i=1; i<=NF; i++) print $i}' | awk -F\> '{print $2}'` 
dan lihat hasilnya. Hasilnya adalah data hasil sql injection.
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_23_28.png)
 
### # Perl Parser
- **Step 1** : Download lesson8.pl pada link berikut [http://www.computersecuritystudent.com/SECURITY_TOOLS/MUTILLIDAE/MUTILLIDAE_2511/lesson8/lesson8.pl.TXT](/http://www.computersecuritystudent.com/SECURITY_TOOLS/MUTILLIDAE/MUTILLIDAE_2511/lesson8/lesson8.pl.TXT)
- **Step 2** : Ganti nama lesson8.pl.TXT menjadi lesson8.pl dan ubah permission menjadi `rwx------` atau 700.
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_39_29.png)
- **Step 3** : Jalankan perintah 
`curl -b crack_cookies.txt -c crack_cookies.txt --user-agent "Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)" --data "page=user-info.php&username=%27+union+select+ccid%2Cccnumber%2Cccv%2Cexpiration%2Cnull+from+credit_cards+--+&password=&user-info-php-submit-button=View+Account+Details" --location "http://10.151.36.64/mutillidae/index.php" | grep -i "Username="  > lesson8.txt`
- **Step 4** : Setelah menjalankan perintah tersebut maka hasil perintah pada **Step 3** disimpan pada file lesson8.txt.
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_42_37.png)
- **Step 5** : Jalankan file lesson8.pl dan lihat hasilnya.
 ![](/assets/lesson-8/VirtualBox_kali_19_12_2017_21_43_37.png)

